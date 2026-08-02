# 日本語 Flashcards (Nihongo)

Web app flashcard học tiếng Nhật — chạy hoàn toàn trong trình duyệt, không cần server.

**🌐 Dùng ngay:** https://thaole29.github.io/nihongo/

## Tính năng
- **Học** — một tab, hai chế độ dùng chung bộ lọc Phân loại / Topic:
  - *Lướt thẻ* — thẻ lật, mặt trước là ký tự (Hiragana / Katakana / Kanji), mặt sau có cách đọc, nghĩa (Anh + Việt), câu ví dụ kèm phiên âm, và note.
  - *Ôn tập (SRS)* — lặp lại ngắt quãng, ưu tiên thẻ hay quên; đảo chiều Ký tự ⇄ Nghĩa. Số thẻ đến hạn hiện ngay trên nút.
- **Trò chuyện** — tán gẫu tiếng Nhật với bot AI. Mỗi phiên app bốc ngẫu nhiên **một trong hai kiểu**, hiện ngay dưới tiêu đề; bấm 🗑 *Cuộc trò chuyện mới* để đổi:
  - *Tán gẫu* — 10 chủ đề (thời tiết, đồ ăn, thú cưng, gia đình…). Bạn chào, bot hỏi lại rồi hai bên nói chuyện tự nhiên.
  - *Đóng vai tình huống* — 8 bối cảnh thật: ☕ quán cà phê · 🏨 lễ tân khách sạn · 🚃 trên tàu điện · 🏪 konbini · 🍜 quán ramen · 🗺️ hỏi đường · 👕 cửa hàng quần áo · 🏫 bạn cùng lớp mới. Bot nhập vai nhân viên/người lạ và dẫn tình huống đi theo đúng các bước ngoài đời (gọi đồ → nóng hay đá → size → tại chỗ hay mang đi → báo giá), dạy bạn những câu **bạn** cần nói khi sang Nhật.
  - **Trình độ N5 / N4** — đổi ở dropdown ngay trên thanh tiêu đề của tab.
  - **Ưu tiên hiragana** — ở N5 bot viết **thuần hiragana**, không kanji (katakana cho từ mượn: コーヒー). N4 mới cho vài kanji cực cơ bản. Câu sửa lỗi giữ nguyên kiểu chữ bạn gõ.
  - **Không lặp trong một phiên** — mỗi lượt bot tự viết một *sổ tay* nén (đã biết gì / đã hỏi gì / đã khen gì) và app gửi trả lại ở lượt sau, nên hội thoại dài bao nhiêu cũng không quên. Bot cũng phải khai báo *kiểu lượt* và không được lặp kiểu của lượt trước — nên nó luân phiên kể chuyện mình, rủ rê, ngạc nhiên, dạy từ mới thay vì lượt nào cũng "khen + hỏi".
  - **Sửa lỗi chính tả / ngữ pháp** kèm giải thích tiếng Việt. App tự đối chiếu câu gốc với câu bot sửa: khác nhau mà bot bảo "đúng rồi" thì vẫn hiện thẻ sửa — không tin has_error của model.
  - Mỗi câu trả lời có romaji + nút 🔊 nghe. Bấm **🇻🇳 Xem nghĩa** ra một lượt cả nghĩa tiếng Việt lẫn **💡 giải thích ngắn gọn điểm ngữ pháp** trong câu (bỏ qua khi câu quá hiển nhiên).
  - Ô nhập có công tắc **gõ romaji → kana**.
- **❓ Hỏi nhanh** — nút tròn ❓ nổi ở góc dưới bên phải, bấm được từ **mọi tab** (phím tắt `Ctrl/⌘ + K`, `Esc` để đóng). Trên máy tính là panel nhỏ neo góc phải, trên điện thoại là tấm trượt lên gần full màn — cùng một khung, chỉ khác cách hiện.
  - Hỏi bằng tiếng Việt: *"「わたしがくせいです」 viết vậy đúng không?"*, *"は và が khác nhau thế nào?"*, *"tại sao lại viết như thế?"*. Trả lời gồm **phán quyết** (✓ đúng · ✗ có lỗi · △ không sai nhưng người Nhật ít nói vậy), **câu đúng** kèm romaji + nghĩa, tối đa 3 điểm ngữ pháp và 2 câu ví dụ có nút 🔊.
  - **Bôi đen** bất kỳ chữ Nhật nào trong app (mặt thẻ, câu ví dụ, tin nhắn chat…) → hiện nút *❓ Hỏi về chỗ này*, khỏi gõ lại.
  - Thẻ sửa lỗi ở tab Trò chuyện có thêm nút **❓ Tại sao?** — hỏi thẳng về đúng câu vừa bị sửa.
  - **💾 Lưu thành thẻ** — biến câu trả lời thành flashcard mới (điền sẵn form Thêm thẻ, bạn xem lại rồi mới lưu).
  - Ưu tiên **độ chính xác** hơn tốc độ: nhiệt độ thấp, không tắt "thinking", ví dụ ưu tiên dùng lại từ đã có trong bộ thẻ của bạn. App còn tự đối chiếu câu bạn hỏi với câu model sửa — lệch nhau mà model bảo "đúng rồi" thì vẫn báo có lỗi. Model không chắc thì hiện dòng cảnh báo ⚠ thay vì đoán bừa.
  - Dùng chung nguồn AI và trình độ N5/N4 với tab Trò chuyện. Lịch sử hỏi đáp lưu trong máy (40 lượt gần nhất), bấm 🗑 để xoá.
- **Nghe phát âm** — dùng giọng đọc tiếng Nhật của trình duyệt (Web Speech API).
- **Thêm thẻ** — gõ romaji tự chuyển kana; chia theo topic. Có nút 📋 copy nhanh romaji / Hiragana / Katakana để dán sang ô khác.
- **Viết tay (thử nghiệm)** — vẽ từng ký tự bằng chuột / ngón tay, app đoán ký tự (dùng dịch vụ nhận dạng Google Input Tools, cần mạng). Bấm kết quả gợi ý để **nối vào ô "câu đang soạn"** rồi vẽ chữ tiếp theo → soạn được **cả cụm từ / câu**. Có dấu cách, xoá ký tự cuối, sửa trực tiếp; xong bấm Copy câu / Tìm trong Quản lý / Điền vào Thêm thẻ.
- **Quản lý** — sửa/xoá, chia trang (50 thẻ/trang) cho gọn & nhanh, thanh tìm kiếm lọc trên toàn bộ thẻ; Export/Import JSON để sao lưu và chuyển máy.

Ưu tiên **Hiragana** mặc định (đổi ở dropdown Phân loại, có ghi nhớ).

## Cài đặt nguồn AI (dùng cho cả Trò chuyện và ❓ Hỏi nhanh)

Chọn nguồn AI trong **💬 Trò chuyện → ⚙️ Cài đặt AI**. Cả hai đều miễn phí:

| | Ai phải có API key | Cần dựng server | Hạn mức |
|---|---|---|---|
| **Google Gemini** (mặc định) | mỗi người tự dán key của mình | không | free tier của Google, không giới hạn thời gian |
| **NVIDIA** | không ai cả — server giữ key hộ | có, Cloudflare Worker (miễn phí) | ~1.000 credit dùng thử của NVIDIA |

Dùng một mình → Gemini là gọn nhất. Muốn người khác vào link là chat được ngay, khỏi đăng ký gì → NVIDIA.

### Cách 1 — Google Gemini (gọi thẳng từ trình duyệt)

1. Lấy API key miễn phí tại https://aistudio.google.com/apikey
2. Mở **⚙️ Cài đặt AI**, chọn nguồn *Google Gemini*, dán key, bấm **Lưu**.

Key nằm trong `localStorage`, **theo từng trình duyệt và từng địa chỉ** — dùng bản GitHub Pages trên máy mới hay điện thoại thì phải dán lại một lần. Key **không** đi kèm Export JSON và **không** đồng bộ lên Google Sheet. Chưa có key thì các tab khác vẫn dùng bình thường.

**Chạy local:** tạo file `config.local.js` cạnh `index.html` để khỏi dán tay:

```js
window.NIHONGO_LOCAL_GEMINI_KEY = 'KEY-CỦA-BẠN';
window.NIHONGO_WORKER_URL = 'http://localhost:8787';   // tuỳ chọn, cho cách 2
```

File này đã nằm trong `.gitignore` nên không bao giờ lên GitHub. ⚠️ **Đừng bao giờ nhét key thẳng vào `index.html`** — repo này public và deploy lên GitHub Pages, key sẽ lộ cho mọi người.

Model dùng được đổi theo tài khoản Google; hiện app hỗ trợ `gemini-3.5-flash` (mặc định), `gemini-3.6-flash`, `gemini-3.1-flash-lite`. Nếu Google ngừng một model, app báo lỗi và bạn chọn model khác trong ⚙️ Cài đặt AI.

### Cách 2 — NVIDIA qua Cloudflare Worker (người dùng không cần key)

NVIDIA chặn CORS nên trình duyệt không gọi thẳng được, và API key thì không thể để trong `index.html`. Vì vậy có `worker/` — một Cloudflare Worker giữ key ở phía server.

Chi phí **0đ**: Workers free 100.000 request/ngày, cho sẵn tên miền `*.workers.dev`, không cần thẻ tín dụng; key NVIDIA lấy free ở https://build.nvidia.com cũng không cần thẻ.

Deploy 5 phút — xem [`worker/README.md`](worker/README.md). Xong thì dán URL worker vào hằng số `CHAT_WORKER_URL` trong `index.html` (URL không phải bí mật, cứ commit) là mọi người mở app dùng được ngay; hoặc để trống rồi tự dán trong ⚙️ Cài đặt AI.

Worker chỉ nhận request từ domain trong whitelist, tự dựng system prompt (nên lấy được URL cũng chỉ chat tiếng Nhật được, không biến thành ChatGPT free), và rate limit theo IP. Client gửi **chỉ số** chủ đề chứ không gửi chuỗi, nên không nhét được nội dung tuỳ ý vào prompt. Danh sách model đổ từ `GET /models` nên không cần sửa app khi NVIDIA thêm/bỏ model.

Model mặc định `openai/gpt-oss-120b` — đo ngày 25/07/2026 trên 6 ca lỗi tiếng Nhật thật (thiếu kana, trường âm, trợ từ, chia động từ, + 1 câu đúng): bắt đúng **6/6**, giải thích tiếng Việt đủ 5/5, phản hồi **2,9–4,3s** qua worker. `qwen/qwen3-next-80b-a3b-instruct` cũng 6/6 nhưng thiếu 1 giải thích và chậm hơn; `meta/llama-3.3-70b-instruct` hay `ResourceExhausted`. Lưu ý: `/models` liệt kê ~91 model nhưng **không phải model nào cũng phục vụ được ở gói free** — gặp `qwen3.5-397b`, `glm-5.2`, `kimi-k2.6` trả 404; app báo lỗi rõ và bạn chọn model khác.

⚠️ Đang dùng NVIDIA mà **Hỏi nhanh** báo *"Server chưa có tính năng Hỏi nhanh"* → worker đang chạy bản cũ, chưa có route `POST /ask`. Deploy lại (`npx wrangler deploy` trong `worker/`) là xong. Đường Gemini không cần làm gì.

⚠️ System prompt nằm ở **hai nơi** cho mỗi tính năng — `chatSystemPrompt()` / `askSystemPrompt()` trong `index.html` (đường Gemini) và `systemPrompt()` / `askSystemPrompt()` trong `worker/nihongo-worker.js` (đường NVIDIA). Sửa một bên nhớ sửa bên kia.

## Dữ liệu
- Lưu trong `localStorage` của trình duyệt (theo từng thiết bị).
- Mở lần đầu trên một máy sẽ tự nạp bộ mặc định trong `deck.js` (46 chữ Hiragana gốc + 60 từ vựng vỡ lòng).
- **Đồng bộ giữa các máy:** dùng **Quản lý → Export JSON** rồi **Import JSON** ở máy kia (giữ nguyên tiến độ học).

## Bộ thẻ
- `deck.js` — bộ mặc định nhúng sẵn (nạp tự động).
- `hiragana_kana.json` — 46 chữ Hiragana あ–ん (có mẹo nhớ hình dạng).
- `starter_vocab.json` — 60 từ vựng cơ bản (Chào hỏi / Đồ ăn / Thời tiết / Đồ trong nhà / Du lịch).

Bộ mặc định hiện có **353 thẻ** trên 21 topic. Thêm thẻ mới vào `deck.js` thì máy đã dùng app cũng nhận được: `mergeNewDefaults()` gộp thẻ chưa có theo `char`, giữ nguyên tiến độ SRS của thẻ cũ và **không** dựng lại thẻ bạn đã chủ động xoá.

Import không tạo bản trùng (upsert theo ký tự, giữ nguyên tiến độ SRS).

## Chạy local
Chỉ cần mở `index.html` bằng trình duyệt.
