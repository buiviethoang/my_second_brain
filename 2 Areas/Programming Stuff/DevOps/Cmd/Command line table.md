Tên cmd hay dùng | Cú pháp | Tên cmd hay dùng | Cú pháp 
------ | ---- | ------ | ----
Tạo new file | **touch filename** | Hiển thị dung lượng RAM còn trống | **free -m**
Tạo new directory for git | mkdir | Mở file | gedit filename
Dùng 1 service đang chạy | sudo service [name] stop | Xóa bỏ 1 chương trình từ ubuntu | sudo apt-get/apt remove [name]
Xóa bỏ unused packages và dependencies | sudo apt-get autoremove | Xóa file/folder, ignore non-existent files, never prompt(cả các file bên trong) | (sudo) rm -rf [name] 
Xóa file/folder -r = to remove directories and their contents recursively |  | Xóa file/folder -v = to explain what is being done
Thêm package vào PATH | export PATH = ~/namepackage/bin:$PATH | Kiểm tra trạng thái các dịch vụ | (sudo) systemctl status [sv_name]
Khởi động dịch vụ | systemctl start [sv_name] | Hiển thị kiểm RAM và tốc độ | sudo lshw -c memory
Liệt kê service mà chạy trong startup | service --status-all | Show bảng router | route -n 
Show user đã đăng nhập vào hệ thống | w | Xóa cache tạm thời (rọn rác hệ thống) | sudo apt-get clean
Hủy bỏ kernel (dọn rác hệ thống) | sudo apt-get autoremove -purge | Show ubuntu version | lsb_release -a
Auto create requirement file | pip(3) freeze > requirement.txt | Cài đặt packages theo file requirement.txt | pip(3) install -re requirements.txt
Reset dịch vụ | systemctl reset [name] | Save packages to a specific folder | pip(3) install package_name -t /your_directory
Sửa lỗi snap changes: xem tiến trình | snap changes | Sửa snap: abort tiến trình | snap abort ID_doing_process
Show user đang nắm quyền | whoami | Chỉ ra những cmd đã dùng trước đó | history  tail: 10 cmd cuối <br> 
Chuyển đổi user | su [tên user] | Thêm user mới vào hệ thống | sudo useradd new_account_name 
Thiết lập mật khẩu cho user mới | sudo passwd new_account_name => nhập | Thêm nhóm người dùng mới | sudo groupadd new_group_name 
Thêm tài khoản vào nhóm | usemod -aG group_name account_name | Liệt kê các nhóm người dùng | getent group 
Xem danh sách người dùng trong 1 nhóm | getent group group_name | Xóa nhóm | groupdel groupname
Show tất cả folder file trong đường dẫn hiện tại | ls -l(a) | Edit nội dung file | getdit/nane file_name
Change umask config | nano/gedit /etc/profile hoặc umask 0027 | Hiển thị kiểu RAM và tốc độ | sudo lshw -c memory
Liệt kê dịch vụ trong startup | service -status-all | show bảng router | route -n
Show user đã đang nhập vào hệ thống | w | Xóa cache tạm thời | sudo apt-get clean
Hủy bỏ kernel | sudo apt-get autoremove -purge | Show ubuntu version | lsb_release -a
Xem nội dung 1 file | cat /path_to_file | Di chuyển file | mv old_path new_path 
Biên tập file với vim | vi file_path | Tìm 1 cụm từ trong file/dòng | grep
Xem các biến môi trường | echo $PATH | Xem path đến 1 executabl file | which ten_file
Who are you | whoami | Who is logged in | users/who/w
Làm việc với nguồn | poweroff/reboot/shutdown | Counting words in a file | wc file_name (num_of_line, num_of_word, num_of_bytes, file_name)
Show process | ps -f | Stop process | Kill (-9) PID 
Show  processes sorted by various criteria.  | top 