# Nihongo chat proxy (Cloudflare Worker)

Cầu nối giữa app và **NVIDIA NIM API**. Nhờ nó, người vào
https://thaole29.github.io/nihongo/ chat được ngay mà **không phải tự đăng ký API key**.

Vì sao phải có worker:
- NVIDIA chặn CORS → trình duyệt không gọi thẳng được.
- API key không thể nhét vào `index.html` (repo public, GitHub Pages → lộ key).

## Chi phí: 0đ

| | Free tier | Cần thẻ? |
|---|---|---|
| Cloudflare Workers | 100.000 request/ngày, không hết hạn | Không |
| Tên miền | `ten-cua-ban.workers.dev` cho sẵn | Không |
| NVIDIA build.nvidia.com | ~1.000 credit dùng thử, ~40 request/phút | Không |

Vượt 100k request/ngày mới phải lên gói $5/tháng — app cá nhân không chạm tới.
Cái hết trước là **credit NVIDIA**, không phải hạn mức Cloudflare.

## Deploy (5 phút)

```bash
# 1. Lấy API key NVIDIA
#    https://build.nvidia.com → đăng nhập → chọn model bất kỳ → "Get API Key"
#    Key có dạng nvapi-xxxxx

# 2. Cài wrangler + đăng nhập Cloudflare (mở trình duyệt 1 lần)
npm install -g wrangler
wrangler login

# 3. Nạp key vào secret (KHÔNG bao giờ nằm trong git)
cd worker
wrangler secret put NVIDIA_API_KEY      # dán nvapi-... rồi Enter

# 4. Deploy
wrangler deploy
```

Wrangler in ra URL kiểu `https://nihongo-chat.<tên-bạn>.workers.dev`. Kiểm tra:

```bash
curl https://nihongo-chat.<tên-bạn>.workers.dev/
# {"ok":true,"service":"nihongo-chat-proxy"}
```

## Nối vào app

Mở `index.html`, tìm hằng số gần đầu phần chat rồi dán URL vào:

```js
const CHAT_WORKER_URL = 'https://nihongo-chat.<tên-bạn>.workers.dev';
```

URL worker **không phải bí mật** — cứ commit lên GitHub. Key nằm trong secret của
Cloudflare, không đi kèm URL.

Xong: mọi người mở app → ⚙️ Cài đặt AI → chọn **NVIDIA (qua server riêng)** là chat được.
Không dán URL vào `index.html` thì vẫn tự dán tay trong ⚙️ Cài đặt AI (lưu localStorage).

## Chống xài chùa

URL worker public, ai biết cũng gọi được. Ba lớp chặn đã có sẵn trong code:

1. **Origin whitelist** — chỉ `thaole29.github.io` + localhost. Trang lạ nhúng app sẽ bị 403.
   Đổi danh sách ở `ALLOWED_ORIGINS` trong `wrangler.toml`.
2. **Prompt cứng server-side** — worker chỉ biết làm một việc: tán gẫu tiếng Nhật + bắt lỗi.
   Client không gửi system prompt lên, nên lấy được URL cũng không biến nó thành ChatGPT free được.
3. **Rate limit theo IP** — 12 request/phút, 120/giờ (`LIMITS` trong `nihongo-worker.js`).

Lớp 3 đếm trong RAM của isolate nên chỉ là *best effort* — Cloudflare tái tạo isolate thì
bộ đếm reset. Muốn trần cứng thì thêm rule ở dashboard (gói Free được 1 rule):

> Cloudflare dashboard → Workers & Pages → chọn worker → **Settings → Rate limiting**
> hoặc Security → WAF → Rate limiting rules → ví dụ 30 request / 1 phút / IP.

Nếu thấy credit tụt bất thường: `wrangler tail` để xem log realtime, hoặc rotate key
(`wrangler secret put NVIDIA_API_KEY` lần nữa với key mới).

## Đổi model

App tự hỏi worker `GET /models` để đổ dropdown, nên **không cần sửa code khi NVIDIA thêm/bỏ model**.
Muốn đổi model mặc định thì sửa `DEFAULT_MODEL` trong `wrangler.toml` rồi `wrangler deploy`.

Đo thử ngày 25/07/2026 (1 lượt chat, từ lúc gửi tới lúc có JSON hoàn chỉnh):

| Model | Thời gian | Kết quả |
|---|---|---|
| `qwen/qwen3-next-80b-a3b-instruct` ← mặc định | 8,6s | bắt lỗi đúng, câu tiếng Nhật tự nhiên |
| `nvidia/llama-3.3-nemotron-super-49b-v1.5` | 15,2s | đúng, chậm hơn |
| `meta/llama-3.3-70b-instruct` | — | `ResourceExhausted` — model này hay quá tải |

Model reasoning (dòng thinking / `deepseek-*-pro`) chạy được (worker tự bóc `<think>`) nhưng
chậm và tốn credit hơn hẳn. Model quá tải thì app báo "Model đang quá tải bên NVIDIA" —
chọn model khác trong ⚙️ Cài đặt AI là xong.

## Sửa prompt

⚠️ System prompt tồn tại ở **hai nơi**:
- `index.html` → `chatSystemPrompt()` — dùng cho đường đi Gemini
- `worker/nihongo-worker.js` → `systemPrompt()` — dùng cho đường đi NVIDIA

Sửa một bên thì phải sửa bên kia, rồi `wrangler deploy` lại worker.

## API

```
GET  /          → {ok:true}
GET  /models    → {models:[...], default:"..."}          (cache 1h)
POST /chat      → body {level:"n5"|"n4", model?:"...", messages:[{role:"user"|"bot", text:"..."}]}
                  trả  {check:{has_error,corrected,error_type,explain_vi}, reply, romaji, vi, model}
                  lỗi  {error:"…"} kèm HTTP 4xx/5xx
POST /ask       → body {level:"n5"|"n4", model?:"...", question:"…", deck?:"…"}   (tab ❓ Hỏi nhanh)
                  trả  {subject, verdict, corrected, corrected_romaji, corrected_vi,
                        answer_vi, points:[{point,detail}], examples:[{jp,romaji,vi}], caveat, model}
                  lỗi  {error:"…"} kèm HTTP 4xx/5xx
```

`/ask` là tra cứu chứ không phải tán gẫu nên đi tham số khác `/chat`: `temperature 0.2`,
`reasoning_effort: 'medium'`, `max_tokens 6000` — chậm hơn vài giây nhưng đúng hơn.
`question` cắt ở 400 ký tự, `deck` (vài thẻ liên quan client gửi kèm để ví dụ bám vốn từ
người học) cắt ở 600 và được đánh dấu là dữ liệu, không phải mệnh lệnh.

⚠️ Worker đang chạy bản cũ thì `/ask` trả 404 và app báo *"Server chưa có tính năng Hỏi
nhanh"* — deploy lại là xong.
