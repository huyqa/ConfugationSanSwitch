
Đây là một hướng dẫn cơ bản cho việc cấu hình một switch SAN Cisco MDS 9148S:

1. Kết nối và cấu hình cơ bản:
Kết nối với switch bằng cổng console bằng cách sử dụng cáp console và một chương trình kết nối như PuTTY.

Đăng nhập vào switch bằng tên người dùng và mật khẩu mặc định hoặc đã được cấu hình trước.

Chuyển sang chế độ cấu hình bằng cách nhập lệnh:
``` switch# configure terminal ``` 
2. Thiết lập cổng và VSAN:
Cấu hình cổng:
```
switch(config)# interface fc1/1
switch(config-if)# switchport mode N (N là mode bạn muốn cấu hình, như switchport mode trunk hoặc switchport mode access)
```
Cấu hình VSAN:
```
switch(config)# vsan database
switch(config-vsan-db)# vsan <VSAN_ID> (VSAN_ID là số ID của VSAN)
switch(config-vsan-db)# vsan <VSAN_ID> interface fc1/1 (gán cổng vào VSAN)
```
3. Zoning:
Tạo zone:
```
switch(config)# zone name example_zone vsan <VSAN_ID> 
```
Thêm các thành viên vào zone:

```
switch(config-zone)# member pwwn <WWN_of_device> ```
Tạo zone set và gán zone vào zone set:
```
switch(config)# zone set name example_zoneset vsan <VSAN_ID>
switch(config-zoneset)# member example_zone
```
Kích hoạt zone set trên các cổng:
```
switch(config)# zoneset activate name example_zoneset vsan <VSAN_ID>
```
4. Lưu cấu hình và thoát:
Lưu cấu hình:

```
switch(config)# exit
switch# copy running-config startup-config
```
Thoát khỏi chế độ cấu hình:

```
switch# exit
```
Lưu ý: Trong các lệnh trên, thay thế các thông số như <VSAN_ID> bằng giá trị thực tế. Cũng cần thay thế <WWN_of_device> bằng địa chỉ World Wide Name của các thiết bị lưu trữ mà bạn muốn thêm vào zone. Đảm bảo sao lưu cấu hình sau khi hoàn thành để tránh mất thông tin cấu hình khi khởi động lại switch.