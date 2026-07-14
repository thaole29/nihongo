# Kết nối Nihongo Flashcards với Google Drive (đồng bộ đa thiết bị)

Mục tiêu: tạo một **OAuth Client ID** để app được phép lưu 1 file dữ liệu vào **thư mục ẩn riêng của app** trong Google Drive của bạn (appDataFolder — không làm rác Drive, không ai khác thấy).

Toàn bộ làm **một lần**, ~10 phút. Không tốn phí, không cần thẻ tín dụng.

---

## Bước 1 — Tạo project trên Google Cloud
1. Mở https://console.cloud.google.com/ và đăng nhập bằng Gmail của bạn.
2. Trên thanh trên cùng, bấm hộp chọn project → **New Project**.
3. Đặt tên `Nihongo Flashcards` → **Create**. Chờ vài giây, rồi chọn project đó.

## Bước 2 — Bật Google Drive API
1. Menu trái → **APIs & Services → Library** (hoặc mở https://console.cloud.google.com/apis/library ).
2. Tìm **Google Drive API** → bấm vào → **Enable**.

## Bước 3 — Cấu hình màn hình đồng ý (OAuth consent screen)
1. Menu trái → **APIs & Services → OAuth consent screen** (console mới có thể nằm ở mục **Google Auth Platform → Branding / Audience**).
2. **User type / Audience: External** → Create/Next.
3. Điền tối thiểu:
   - **App name:** `Nihongo Flashcards`
   - **User support email:** email của bạn
   - **Developer contact:** email của bạn
   - Các mục logo/domain có thể để trống.
4. **KHÔNG bấm Publish.** Giữ trạng thái **Testing**.
5. Vào mục **Test users → Add users** → thêm chính **email Gmail của bạn** → Save.
   > Quan trọng: chỉ email nằm trong Test users mới đăng nhập được. Đúng như mong muốn (chỉ mình bạn sync).

## Bước 4 — Tạo OAuth Client ID
1. Menu trái → **APIs & Services → Credentials**.
2. **+ Create Credentials → OAuth client ID**.
3. **Application type: Web application**.
4. **Name:** `Nihongo Web`.
5. Ở **Authorized JavaScript origins → + Add URI**, thêm chính xác (không có dấu `/` ở cuối):
   ```
   https://thaole29.github.io
   ```
   (Tuỳ chọn, nếu muốn test trên máy: thêm `http://localhost:8000`.)
6. **Authorized redirect URIs:** để trống cũng được (app dùng luồng token popup, không cần redirect).
7. **Create** → hiện hộp thoại có **Client ID** dạng:
   ```
   1234567890-abcdefg.apps.googleusercontent.com
   ```
8. **Copy Client ID** đó lại.

## Bước 5 — Gửi Client ID cho mình
Dán Client ID vào chat. Mình sẽ tích hợp nút **"Kết nối Google Drive"** + đồng bộ (kéo khi mở app, đẩy khi có thay đổi, bản mới nhất thắng).

> Client ID là thông tin **công khai an toàn**, không phải mật khẩu — nhúng vào trang public không sao. Bảo mật dựa trên đăng nhập Google + phạm vi `drive.appdata` (chỉ đụng được file do app tạo).

---

## Lưu ý / khắc phục sự cố
- **Màn hình "Google chưa xác minh ứng dụng này":** bình thường với app ở chế độ Testing. Bấm **Advanced → Go to Nihongo Flashcards (unsafe)** để tiếp tục (an toàn vì app là của chính bạn).
- **Phải đăng nhập lại sau ~1 giờ:** token Google hết hạn theo phiên; bấm lại nút Đồng bộ là xong.
- **Đổi origin:** nếu sau này dùng tên miền khác, nhớ thêm origin đó vào bước 4.5.
- **file:// không dùng được OAuth** — phải chạy trên `https://thaole29.github.io` (hoặc `http://localhost:PORT`).
