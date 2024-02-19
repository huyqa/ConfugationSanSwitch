1. Xác thực và ủy quyền:
Sử dụng xác thực bằng tên người dùng và mật khẩu mạnh:
arduino
Copy code
switch(config)# username admin password strong_password
Kích hoạt AAA và cấu hình để sử dụng xác thực bằng tên người dùng:
arduino
Copy code
switch(config)# aaa new-model
switch(config)# aaa authentication login default local
2. SSH và Telnet:
Tắt Telnet và chỉ sử dụng SSH:
arduino
Copy code
switch(config)# line vty 0 4
switch(config-line)# transport input ssh
3. ACLs (Access Control Lists):
Áp dụng ACLs để kiểm soát truy cập vào các dịch vụ như Telnet, SSH, SNMP:
arduino
Copy code
switch(config)# ip access-list standard MANAGEMENT_ACCESS
switch(config-std-nacl)# permit 10.0.0.0 0.255.255.255
switch(config-std-nacl)# permit 192.168.0.0 0.0.255.255
switch(config)# line vty 0 4
switch(config-line)# access-class MANAGEMENT_ACCESS in
4. Secure Management Access:
Sử dụng VLAN quản trị và giới hạn truy cập từ các địa chỉ IP quản trị:
arduino
Copy code
switch(config)# interface vlan 10
switch(config-if)# ip address 10.0.0.1 255.255.255.0
switch(config)# ip access-list standard MANAGEMENT_ACCESS
switch(config-std-nacl)# permit 10.0.0.0 0.255.255.255
5. Cập nhật phần mềm:
Kiểm tra và cập nhật phần mềm của switch:
arduino
Copy code
switch# show version
switch# install all kickstart <kickstart_image_file> system <system_image_file> kickstart <kickstart_image_file> module <module_image_file>
6. Giám sát và ghi nhật ký:
Kích hoạt logging và giám sát sự kiện quan trọng:
arduino
Copy code
switch(config)# logging server 192.168.0.10
switch(config)# logging facility local6
7. Disable không cần thiết:
Tắt các dịch vụ không cần thiết như CDP:
arduino
Copy code
switch(config)# no cdp run
8. Mã hóa dữ liệu:
Sử dụng HTTPS để quản lý từ xa:
arduino
Copy code
switch(config)# ip http secure-server
9. Bảo vệ các cấu hình:
Sao lưu và bảo vệ cấu hình:
lua
Copy code
switch# copy running-config startup-config
Lưu ý rằng các cấu hình cụ thể có thể phụ thuộc vào môi trường mạng cụ thể của bạn và nên được điều chỉnh phù hợp để đáp ứng các yêu cầu bảo mật và kỹ thuật của tổ chức.