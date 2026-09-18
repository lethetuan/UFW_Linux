# UFW_Linux

# Hướng dẫn cơ bản về UFW (Uncomplicated Firewall)

UFW (Uncomplicated Firewall) là một công cụ quản lý tường lửa mặc định trên các bản phân phối Linux như Ubuntu và Debian. Nó được thiết kế với giao diện dòng lệnh tối giản nhằm giúp đơn giản hóa việc cấu hình tường lửa phức tạp.

Firewall trên Ubuntu cũng tương tự như Windows Firewall trên hệ điều hành Windows, đều là tường lửa mềm (software firewall).

## Các câu lệnh dùng để quản lý dịch vụ UFW trên Linux thường dùng.

**Kiểm tra tình trạng hoạt động của UFW**
```bash
systemctl status ufw
```

**Bắt đầu (start) dịch vụ UFW**
```bash
systemctl start ufw
```

**Cho phép UFW tự động start khi server khởi động lại**
```bash
systemctl enable ufw
```

**Không cho UFW tự động start khi server khởi động lại**
```bash
systemctl disable ufw
```

## Cấu hình cho phép kết nối (Allow)

*Lưu ý: Trong nội dung gốc, lệnh mở port ghi là `systemctl ufw allow...`, tuy nhiên cú pháp chính xác của UFW để mở port là `ufw allow...`. Tài liệu này đã điều chỉnh lại cho chính xác.*

**Demo cấu hình cho phép kết nối theo tên dịch vụ/protocol**
*(Ví dụ: chữ "ssh" - có thể thay bằng tên các dịch vụ khác muốn mở)*
```bash
ufw allow ssh
```

**Demo cấu hình cho phép kết nối đến server linux theo port cụ thể**
*(Ví dụ: mở port cho dịch vụ web HTTP và HTTPS)*
```bash
ufw allow 80/tcp
ufw allow 443/tcp
```

**Khởi động lại để áp dụng cấu hình (Apply config)**
```bash
systemctl restart ufw
```
*(Lưu ý: Bạn cũng có thể dùng lệnh `ufw reload` để tải lại cấu hình tường lửa mà không cần khởi động lại toàn bộ dịch vụ).*

---
**Một số port và dịch vụ thông dụng:**
- **22/tcp**: SSH
- **80/tcp**: HTTP (Web)
- **443/tcp**: HTTPS (Web bảo mật)
- **21/tcp**: FTP
- **3306/tcp**: MySQL
