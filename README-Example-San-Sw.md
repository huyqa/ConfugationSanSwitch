Cấu hình mẫu cho một switch SAN Cisco MDS 9148S. Trong ví dụ này, chúng tôi sẽ thiết lập ba cổng và một VSAN, sau đó tạo một zone và gán một thiết bị lưu trữ vào zone đó. Đảm bảo thay thế các giá trị thực tế như địa chỉ MAC và địa chỉ IP theo yêu cầu của bạn:

```
! Bắt đầu cấu hình
switch# configure terminal

! Thiết lập cổng fc1/1, fc1/2, fc1/3 và fc1/4 và gán chúng vào VSAN 100
switch(config)# interface fc1/1
switch(config-if)# switchport mode F
switch(config-if)# interface fc1/2
switch(config-if)# switchport mode F
switch(config-if)# interface fc1/3
switch(config-if)# switchport mode F
switch(config-if)# interface fc1/4
switch(config-if)# switchport mode F

! Thiết lập VSAN 100
switch(config)# vsan database
switch(config-vsan-db)# vsan 100
switch(config-vsan-db)# vsan 100 interface fc1/1
switch(config-vsan-db)# vsan 100 interface fc1/2
switch(config-vsan-db)# vsan 100 interface fc1/3
switch(config-vsan-db)# vsan 100 interface fc1/4

! Tạo zone và thêm thiết bị lưu trữ vào zone
switch(config)# zone name storage_zone vsan 100
switch(config)# zone member pwwn 50:00:14:42:32:21:34:34 vsan 100

! Tạo zone set và thêm zone vào zone set
switch(config)# zoneset name storage_zoneset vsan 100
switch(config-zoneset)# member storage_zone

! Kích hoạt zone set trên các cổng
switch(config)# zoneset activate name storage_zoneset vsan 100

! Lưu cấu hình và thoát
switch(config)# exit
switch# copy running-config startup-config
switch# exit
```

Vui lòng thay đổi các giá trị như địa chỉ MAC (pwwn) và VSAN ID (vsan) phù hợp với môi trường của bạn. Đây chỉ là một ví dụ cơ bản và cần được tinh chỉnh theo yêu cầu cụ thể của mạng lưu trữ.