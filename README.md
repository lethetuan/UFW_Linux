# Hướng dẫn cơ bản về UFW (Uncomplicated Firewall) trên hệ điều hành Linux

UFW (Uncomplicated Firewall) là một công cụ quản lý tường lửa mặc định trên các bản phân phối Linux như Ubuntu và Debian. Nó được thiết kế với giao diện dòng lệnh tối giản nhằm giúp đơn giản hóa việc cấu hình tường lửa phức tạp.

Firewall trên Ubuntu cũng tương tự như Windows Firewall trên hệ điều hành Windows, đều là tường lửa mềm (software firewall).

## Các câu lệnh dùng để quản lý dịch vụ UFW trên Linux thường dùng.

**Kiểm tra tình trạng hoạt động của UFW**
```bash
sudo systemctl status ufw
```

**Bắt đầu (start) dịch vụ UFW**
```bash
sudo systemctl start ufw
```

**Cho phép UFW tự động start khi server khởi động lại**
```bash
sudo systemctl enable ufw
```

**Không cho UFW tự động start khi server khởi động lại**
```bash
sudo systemctl disable ufw
```

## Cấu hình cho phép kết nối (Allow)

*Lưu ý: Trong nội dung gốc, lệnh mở port ghi là `systemctl ufw allow...`, tuy nhiên cú pháp chính xác của UFW để mở port là `ufw allow...`. Tài liệu này đã điều chỉnh lại cho chính xác.*

**Demo cấu hình cho phép kết nối theo tên dịch vụ/protocol**
*(Ví dụ: chữ "ssh" - có thể thay bằng tên các dịch vụ khác muốn mở)*
```bash
sudo ufw allow ssh
```

**Demo cấu hình cho phép kết nối đến server linux theo port cụ thể**
*(Ví dụ: mở port cho dịch vụ web HTTP và HTTPS)*
```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

**Khởi động lại để áp dụng cấu hình (Apply config)**
```bash
sudo systemctl restart ufw
```
*(Lưu ý: Bạn cũng có thể dùng lệnh `ufw reload` để tải lại cấu hình tường lửa mà không cần khởi động lại toàn bộ dịch vụ).*

**Cách này sẽ gỡ bỏ hoàn toàn cấu hình "allow" mà bạn đã thêm vào trước đó, đưa cổng/dịch vụ đó về trạng thái mặc định của tường lửa (thường là chặn từ bên ngoài vào).

Kiểm tra danh sách trạng thái các cổng firewall đang cấu hình
```bash
sudo ufw status
```

**Cách 1: Xóa theo tên dịch vụ hoặc port. Ví dụ xóa quyền cho phép dịch vụ SSH. Cú pháp rất đơn giản, bạn chỉ cần thêm chữ delete vào trước lệnh allow cũ.
```bash
sudo ufw delete allow ssh
sudo ufw reload
```

**Cách 2: Xóa quyền cho phép port 80

```bash
sudo ufw delete allow 80/tcp
sudo ufw reload
```


---
<img width="1024" height="622" alt="image" src="https://github.com/user-attachments/assets/ebf0c1c2-c232-48c0-8983-85b7c4f44af2" />

**Một số port và dịch vụ thông dụng:**
- **22/tcp**: SSH
- **80/tcp**: HTTP (Web)
- **443/tcp**: HTTPS (Web bảo mật)
- **21/tcp**: FTP
- **3306/tcp**: MySQL
<img width="734" height="1024" alt="image" src="https://github.com/user-attachments/assets/04cb8205-a19c-41e2-8896-18d7a96e91f8" />

