# 日本語 Flashcards (Nihongo)

Web app flashcard học tiếng Nhật — chạy hoàn toàn trong trình duyệt, không cần server.

**🌐 Dùng ngay:** https://thaole29.github.io/nihongo/

## Tính năng
- **Học** — thẻ lật, mặt trước là ký tự (Hiragana / Katakana / Kanji), mặt sau có cách đọc, nghĩa (Anh + Việt), câu ví dụ kèm phiên âm, và note.
- **Ôn tập (SRS)** — lặp lại ngắt quãng, ưu tiên thẻ hay quên; đảo chiều Ký tự ⇄ Nghĩa.
- **Quiz** — gõ cách đọc / trắc nghiệm nghĩa / trắc nghiệm ngược, có chấm điểm.
- **Nghe phát âm** — dùng giọng đọc tiếng Nhật của trình duyệt (Web Speech API).
- **Thêm thẻ** — gõ romaji tự chuyển kana; chia theo topic.
- **Quản lý** — sửa/xoá, Export/Import JSON để sao lưu và chuyển máy.

Ưu tiên **Hiragana** mặc định (đổi ở dropdown Phân loại, có ghi nhớ).

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
