# Đồng bộ Nihongo Flashcards qua Google Sheet

Mục tiêu: tạo **OAuth Client ID** để app được phép tạo & ghi **một Google Sheet** trong Drive của bạn làm nơi đồng bộ. App tự tạo sheet tên `Nihongo Flashcards` ở lần đồng bộ đầu (bạn **không** phải tạo tay).

Làm **một lần**, ~10 phút. Miễn phí, không cần thẻ tín dụng.

---

## Bước 1 — Tạo project
1. Mở https://console.cloud.google.com/ → đăng nhập Gmail của bạn.
2. Thanh trên cùng → hộp chọn project → **New Project**.
3. Tên `Nihongo Flashcards` → **Create** → chọn project đó.

## Bước 2 — Bật API (BẬT CẢ HAI)
Menu trái → **APIs & Services → Library**, bật lần lượt:
1. **Google Sheets API** → Enable.
2. **Google Drive API** → Enable.
   > Cần cả hai: Sheets API để đọc/ghi ô, Drive API để tìm lại đúng file sheet trên máy khác.

## Bước 3 — OAuth consent screen
1. Menu trái → **APIs & Services → OAuth consent screen** (console mới: **Google Auth Platform → Branding / Audience**).
2. **User type / Audience: External** → Create/Next.
3. Điền tối thiểu:
   - **App name:** `Nihongo Flashcards`
   - **User support email:** email của bạn
   - **Developer contact:** email của bạn
4. **KHÔNG Publish** — giữ trạng thái **Testing**.
5. **Test users → Add users → thêm email Gmail của bạn** → Save.
   > Chỉ email trong Test users mới đăng nhập được (đúng ý: chỉ mình bạn sync).

## Bước 4 — Tạo OAuth Client ID
1. Menu trái → **APIs & Services → Credentials**.
2. **+ Create Credentials → OAuth client ID**.
3. **Application type: Web application**, Name: `Nihongo Web`.
4. **Authorized JavaScript origins → + Add URI** (không có `/` ở cuối):
   ```
   https://thaole29.github.io
   ```
   (Tuỳ chọn để test local: thêm `http://localhost:8000`.)
5. **Authorized redirect URIs:** để trống (dùng luồng token popup).
6. **Create** → copy **Client ID** dạng:
   ```
   1234567890-abcdefg.apps.googleusercontent.com
   ```

## Bước 5 — Gửi Client ID cho mình
Dán Client ID vào chat. Mình sẽ gắn nút **"Kết nối Google Sheet"** + đồng bộ vào app.

---

## Dữ liệu trong Sheet trông thế nào
App tạo sheet với dòng 1 là tiêu đề cột:

| type | topic | char | reading | meaning | example | note | srs |
|------|-------|------|---------|---------|---------|------|-----|

- Mỗi dòng dưới = 1 thẻ.
- Cột `srs` là chuỗi JSON nhỏ giữ tiến độ ôn tập (không cần đụng tay).
- Bạn có thể **gõ/dán thẳng nhiều dòng vào Sheet** để thêm thẻ hàng loạt → mở app bấm đồng bộ là nhận.

## Đồng bộ hoạt động
- Mở app / bấm **Đồng bộ** → kéo toàn bộ từ Sheet về.
- Thêm/sửa/xoá trong app → tự ghi lại Sheet.
- Quy tắc khi lệch: **bản mới nhất thắng** (theo thời điểm sửa).

## Lưu ý / khắc phục sự cố
- **"Google chưa xác minh ứng dụng":** bình thường ở chế độ Testing → **Advanced → Go to Nihongo Flashcards (unsafe)** (an toàn, app của chính bạn).
- **Giữ đăng nhập lâu (không phải login lại mỗi phiên):** app nhớ đúng tài khoản (email) và **tự làm mới token im lặng** khi bạn mở lại — miễn là bạn **vẫn đang đăng nhập Google trong trình duyệt đó** (Google giữ phiên hàng tuần/tháng nếu chọn "stay signed in"). Access token của Google chỉ sống ~1 giờ và **không có refresh token cho app tĩnh chạy trên trình duyệt**, nên không thể "giữ token cứng 30 ngày" — thay vào đó app làm mới tự động nên bạn gần như không thấy popup. Chỉ phải bấm **Kết nối** lại nếu bạn đăng xuất Google, đổi máy/trình duyệt, hoặc trình duyệt chặn cookie của accounts.google.com (Safari/iOS ITP có thể chặn — khi đó thi thoảng cần bấm lại).
- Chỉ chạy trên `https://thaole29.github.io` (không chạy khi mở file trực tiếp).
- Client ID là thông tin **công khai an toàn**, không phải mật khẩu.
