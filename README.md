# Bài 2: Cấu hình phân quyền Nhóm và sudoers bằng visudo

## 1. Tạo Group

Tạo nhóm `devops-admin`:

```bash
sudo groupadd devops-admin

Kiểm tra:

getent group devops-admin
2. Tạo User

Tạo tài khoản deployer:

sudo adduser deployer

Thêm deployer vào nhóm devops-admin:

sudo usermod -aG devops-admin deployer

Kiểm tra:

groups deployer

Kết quả có nhóm:

devops-admin
3. Cấu hình sudoers bằng visudo

Mở file sudoers:

sudo visudo

Thêm dòng sau vào cuối file:

%devops-admin ALL=(ALL) NOPASSWD: /usr/bin/systemctl start *, /usr/bin/systemctl stop *, /usr/bin/systemctl restart *, /usr/bin/systemctl status *

Quyền trên cho phép các tài khoản thuộc nhóm devops-admin sử dụng:

systemctl start
systemctl stop
systemctl restart
systemctl status

và không cần nhập mật khẩu.

4. Kiểm tra bằng tài khoản deployer

Chuyển sang tài khoản deployer:

su - deployer

Kiểm tra quyền sudo:

sudo -l

Kết quả:

User deployer may run the following commands on Xuan-Chien:
    (ALL) NOPASSWD: /usr/bin/systemctl start *, /usr/bin/systemctl stop *, /usr/bin/systemctl restart *, /usr/bin/systemctl status *
5. Kiểm tra restart dịch vụ cron

Thực hiện:

sudo systemctl restart cron

Lệnh chạy thành công và không yêu cầu nhập mật khẩu.

Kiểm tra trạng thái:

sudo systemctl status cron

Kết quả:

cron.service - Regular background program processing daemon
Active: active (running)
6. Kết luận

Đã hoàn thành yêu cầu của bài:

Tạo group devops-admin.
Tạo user deployer.
Thêm deployer vào group devops-admin.
Cấu hình /etc/sudoers bằng visudo.
Cho phép group devops-admin thực hiện systemctl start, stop, restart, status.
Các lệnh được cấp quyền sử dụng NOPASSWD, không cần nhập mật khẩu.
Kiểm tra thành công lệnh sudo systemctl restart cron.