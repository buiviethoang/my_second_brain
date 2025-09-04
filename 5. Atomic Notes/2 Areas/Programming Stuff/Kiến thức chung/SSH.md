
2025-08-30 09:56
Status: #baby
Tags: [[network]]
## Main

## Định nghĩa: 
SSH, hoặc được gọi là Secure Shell, là một giao thức điều khiển từ xa cho phép người dùng kiểm soát và chỉnh sửa server từ xa qua Internet. Dịch vụ được tạo ra nhằm thay thế cho trình Telnet vốn không có mã hóa và sử dụng kỹ thuật cryptographic để đảm bảo tất cả giao tiếp gửi tới và gửi từ server từ xa diễn ra trong tình trạng mã hóa. Nó cung cấp thuật toán để chứng thực người dùng từ xa, chuyển input từ client tới host, và relay kết quả trả về tới khách hàng.
## Hoạt động
Lệnh SSH có 3 phần:
```bash
ssh {user}@{host}
```
SSH key command cho hệ thống biết là bạn muốn mở một kết nối được mã hóa Secure Shell Connection. **{user}** đại diện cho tài khoản người dùng bạn muốn dùng để truy cập. Ví dụ, bạn muốn truy cập user **root**, thì thay root tại đây. User root là user quản trị hệ thống với toàn quyền để chỉnh sửa bất kỳ điều gì trên hệ thống. **{host}** đại diện cho máy tính bạn muốn dùng để truy cập. Nó có thể là một địa chỉ IP **(ví dụ 244.235.23.19)** hoặc một tên miền (ví dụ, www.xyzdomain.com).

## Kĩ thuật mã hóa 
Lợi điểm khiến SSH hơn hẵn những giao thức cũ là khả năng mã hóa và truyền tải dữ liệu an toàn giữa host và client. **Host** đại diện cho máy chủ  từ xa bạn muốn kết nối tới và **client** là máy tính của bạn dùng để truy cập tới host. Có 3 cách khác nhau để mã hóa qua SSH:
1.  Symmetrical encryption
2.  Asymmetrical encryption
3.  Hashing.

## Một số lệnh thông dụng
###  `ssh-keygen`
`Ssh-keygen` is a tool for creating new authentication key pairs for SSH. Such key pairs are used for automating logins, single sign-on, and for authenticating hosts.
Eg:  `ssh-keygen -t rsa -b 4096`
the `-t` “type” flag to `rsa`, and adds the `-b 4096` “bits” flag to create a 4096 bit key.
Tìm hiểu thêm: 
https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-2

### Copying the Public Key to Your Server
```bash
ssh-copy-id sammy@your_server_address
```



Một số lưu ý liên quan đến SSH
Kiểm tra SSH key có chưa: ls -al ~/.ssh/id_*.pub
Tạo ssh key mới cho Ubuntu:  ssh-key gen -t rsa
Trong đó: -t có nghĩa là type, rsa là giao thức mã hóa
Nếu muốn mạnh hơn: ssh-key gen -t rsa -b 4096 
Trong đó 4096 là số bit khóa

Sau đó nó sẽ hỏi: 
Nhập tên file để lưu (/home/.ssh.id_rsa)
Nhập mật khẩu (bỏ trống nếu không đặt mật khẩu)

Copy public key: 
C1: sử dụng ssh-copy-id command: ssh-copy-id remote_username@remote_IP_Address
Sau đó bạn sẽ nhập mật khẩu máy remote. Sau khi chứng thực đúng, SSH public key sẽ được thêm vào file authorized_keys của máy đó. Kết nối sẽ tự động bị tắt sau khi thêm
C2: Copy private key bằng ssh:
cat ~/.ssh/id_rsa.pub | ssh remote_username@remote_ip_address "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
C3: Thủ công
- B1: Lấy nội dung file id_rsa.pub: cat ~/.ssh/id_rsa.pub
- B2: mkdir -p ~/.ssh
- B3: echo SSH_public_key >> ~/.ssh/authorized_key để thêm public key vào file trống có tên là authorized_key đã tạo sẵn

Sau khi key đc copy
Cấp quyền vào remote server cho .ssh
chmod -766 ~/.ssh


## References
