# 日本語 Flashcards (Nihongo)

Web app flashcard học tiếng Nhật — chạy hoàn toàn trong trình duyệt, không cần server.

**🌐 Dùng ngay:** https://thaole29.github.io/nihongo/

## Tính năng
- **Học** — một tab, hai chế độ dùng chung bộ lọc Phân loại / Topic:
  - *Lướt thẻ* — thẻ lật, mặt trước là ký tự (Hiragana / Katakana / Kanji), mặt sau có cách đọc, nghĩa (Anh + Việt), câu ví dụ kèm phiên âm, và note.
  - *Ôn tập (SRS)* — lặp lại ngắt quãng, ưu tiên thẻ hay quên; đảo chiều Ký tự ⇄ Nghĩa. Số thẻ đến hạn hiện ngay trên nút.
- **Trò chuyện** — tán gẫu tiếng Nhật với bot AI. Mỗi ngày mở tab là một phiên mới: bạn chào, bot hỏi lại một câu rồi hai bên nói chuyện tự nhiên ở mức cơ bản (chọn N5 hoặc N4). Bot **sửa lỗi chính tả / ngữ pháp** kèm giải thích tiếng Việt, mỗi câu trả lời có romaji + nút 🔊 nghe và nút xem nghĩa tiếng Việt. Ô nhập có công tắc **gõ romaji → kana**.
- **Nghe phát âm** — dùng giọng đọc tiếng Nhật của trình duyệt (Web Speech API).
- **Thêm thẻ** — gõ romaji tự chuyển kana; chia theo topic. Có nút 📋 copy nhanh romaji / Hiragana / Katakana để dán sang ô khác.
- **Viết tay (thử nghiệm)** — vẽ từng ký tự bằng chuột / ngón tay, app đoán ký tự (dùng dịch vụ nhận dạng Google Input Tools, cần mạng). Bấm kết quả gợi ý để **nối vào ô "câu đang soạn"** rồi vẽ chữ tiếp theo → soạn được **cả cụm từ / câu**. Có dấu cách, xoá ký tự cuối, sửa trực tiếp; xong bấm Copy câu / Tìm trong Quản lý / Điền vào Thêm thẻ.
- **Quản lý** — sửa/xoá, chia trang (50 thẻ/trang) cho gọn & nhanh, thanh tìm kiếm lọc trên toàn bộ thẻ; Export/Import JSON để sao lưu và chuyển máy.

Ưu tiên **Hiragana** mặc định (đổi ở dropdown Phân loại, có ghi nhớ).

## Cài đặt tab Trò chuyện
Tab Trò chuyện gọi **Google Gemini** (gói miễn phí) trực tiếp từ trình duyệt:

1. Lấy API key miễn phí tại https://aistudio.google.com/apikey
2. Mở tab **💬 Trò chuyện → ⚙️ Cài đặt AI**, dán key, bấm **Lưu**.

Key nằm trong `localStorage`, **theo từng trình duyệt và từng địa chỉ** — dùng bản GitHub Pages trên máy mới hay điện thoại thì phải dán lại một lần. Key **không** đi kèm Export JSON và **không** đồng bộ lên Google Sheet. Chưa có key thì các tab khác vẫn dùng bình thường.

**Chạy local:** tạo file `config.local.js` cạnh `index.html` để khỏi dán tay:

```js
window.NIHONGO_LOCAL_GEMINI_KEY = 'KEY-CỦA-BẠN';
```

File này đã nằm trong `.gitignore` nên không bao giờ lên GitHub. ⚠️ **Đừng bao giờ nhét key thẳng vào `index.html`** — repo này public và deploy lên GitHub Pages, key sẽ lộ cho mọi người.

Model dùng được đổi theo tài khoản Google; hiện app hỗ trợ `gemini-3.5-flash` (mặc định), `gemini-3.6-flash`, `gemini-3.1-flash-lite`. Nếu Google ngừng một model, app báo lỗi và bạn chọn model khác trong ⚙️ Cài đặt AI.

## Dữ liệu
- Lưu trong `localStorage` của trình duyệt (theo từng thiết bị).
- Mở lần đầu trên một máy sẽ tự nạp bộ mặc định trong `deck.js` (46 chữ Hiragana gốc + 60 từ vựng vỡ lòng).
- **Đồng bộ giữa các máy:** dùng **Quản lý → Export JSON** rồi **Import JSON** ở máy kia (giữ nguyên tiến độ học).

## Bộ thẻ
- `deck.js` — bộ mặc định nhúng sẵn (nạp tự động).
- `hiragana_kana.json` — 46 chữ Hiragana あ–ん (có mẹo nhớ hình dạng).
- `starter_vocab.json` — 60 từ vựng cơ bản (Chào hỏi / Đồ ăn / Thời tiết / Đồ trong nhà / Du lịch).

Import không tạo bản trùng (upsert theo ký tự, giữ nguyên tiến độ SRS).

## Chạy local
Chỉ cần mở `index.html` bằng trình duyệt.
