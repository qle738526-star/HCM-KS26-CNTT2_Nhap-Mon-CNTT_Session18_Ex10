## **Bài 10: Đánh Giá Đa Giải Pháp Xác Thực Đa Yếu Tố (2FA)** 

## **Phần 1: Phân tích 2 Giải pháp Xác thực**

### 1\. Phân tích 3 yếu tố xác thực danh tính số

\-Something You Know (Thứ bạn biết): Thông tin ghi nhớ trong đầu (Mật khẩu, mã PIN).  
\-Something You Have (Thứ bạn sở hữu): Thiết bị hoặc vật thể bạn nắm giữ (Điện thoại, thẻ từ, SIM).  
\-Something You Are (Thứ thuộc về bạn): Đặc điểm sinh trắc học (Vân tay, FaceID).

Trong mô hình 2FA:  
\-Mật khẩu (Password): Yếu tố Something You Know.  
\-Mã OTP: Yếu tố Something You Have (chứng minh bạn đang cầm chiếc điện thoại).

### 2\. Nguyên lý hoạt động của Authenticator khi Offline

\-Mật mã chung: Khi quét mã QR lần đầu, điện thoại và máy chủ lưu chung 1 "mật mã bí mật".  
\-Đồng bộ giờ: Cả hai bên cùng dùng đồng hồ hệ thống (thời gian thực).  
\-Tự tính toán độc lập: Cứ 30 giây, app lấy mật mã bí mật kết hợp với giờ hiện tại để tính ra 6 chữ số. Máy chủ ở phía bên kia cũng tính theo đúng cách đó.  
\+App hoàn toàn không cần Wi-Fi/4G/SMS vì mọi phép tính đều diễn ra trực tiếp trên điện thoại.

## **Phần 2: Bảng So sánh Trade-off & Ra quyết định**

### 3\. Bảng so sánh SMS OTP và Authenticator TOTP

| Tiêu chí đánh giá | Giải pháp 1: SMS OTP | Giải pháp 2: TOTP Authenticator |
| ----- | ----- | ----- |
| 1\. Khả năng chống SIM Swapping & SS7 | Kém — Dễ bị kẻ xấu lừa nhà mạng cướp SIM hoặc nghe lén tin nhắn. | Tuyệt đối — Mã lưu an toàn trong chip điện thoại, cướp SIM cũng không lấy được mã. |
| 2\. Tính sẵn sàng khi Offline / Nước ngoài | Phụ thuộc sóng di động — Mất sóng, đi máy bay hoặc ra nước ngoài chưa Roaming sẽ không nhận được mã. | Hoạt động 100% Offline — Sinh mã chính xác mọi lúc mọi nơi, kể cả Chế độ Máy bay. |
| 3\. Tiện dụng & Chi phí vận hành | Dễ dùng nhưng tốn phí — Không cần cài app, nhưng doanh nghiệp tốn tiền mua dịch vụ SMS cho mỗi lần đăng nhập. | Miễn phí 100% & Nhanh chóng — Doanh nghiệp không mất phí viễn thông, thao tác lấy mã trên app cực nhanh. |
| 4\. Rủi ro khi mất điện thoại | Dễ khôi phục nhưng rủi ro cao — Làm lại SIM là lấy lại mã, nhưng kẻ trộm SIM có thể chiếm tài khoản ngay. | Bảo mật cao — Cần dùng Bộ Mã Khôi phục (Backup Codes) để lấy lại quyền truy cập. |

### 4\. Kết luận lựa chọn cho PixelForge Studio

Lựa chọn: bắt buộc dùng giải pháp 2: TOTP Authenticator.

Lý do:

1. Chống bị cướp tài khoản: Kẻ xấu có thể lừa nhà mạng để cướp số điện thoại nhằm lấy mã SMS. Dùng ứng dụng Authenticator sẽ chặn đứng hoàn toàn nguy cơ này vì mã được lưu bảo mật ngay trên chip điện thoại.  
2. Không lo mất sóng: Nhân viên đi công tác nước ngoài hay làm việc trên máy bay không có sóng di động vẫn mở app lấy mã đăng nhập làm việc bình thường.

## **Phần 3: Quản lý Rủi ro & Backup Codes**

### 5\. Quản lý Bộ 10 Mã Khôi phục (Backup Codes)

\-Mục đích: Bộ mã dùng 1 lần này là "chìa khóa dự phòng" duy nhất giúp bạn đăng nhập lại tài khoản để cài lại 2FA khi bị mất, hỏng điện thoại hoặc lỡ xóa app Authenticator.  
2 vị trí lưu an toàn tuyệt đối:

\-Trình quản lý mật khẩu doanh nghiệp: Lưu dạng Encrypted Note trên 1Password hoặc Bitwarden.  
\-In ra giấy: In bộ mã cất vào két sắt hoặc tủ tài liệu có khóa tại nhà/văn phòng.  
1 sai lầm tai hại cần tránh:  
\-Sai lầm: Chụp ảnh màn hình hoặc lưu file text plain (backup\_codes.txt) trên điện thoại, máy tính, hoặc Google Drive cá nhân.  
\-Tác hại: Nếu thiết bị dính virus hoặc tài khoản Cloud bị lộ, kẻ xấu sẽ lấy trọn 10 mã này và vượt qua hoàn toàn lớp bảo vệ 2FA.  
