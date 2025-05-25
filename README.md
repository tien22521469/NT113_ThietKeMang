# NT113-Project

Đồ án Thiết kế Mạng UIT

## Tổng quan

Công ty Outsource O-UIT có 1 trụ sở chính tại Thủ Đức và một chi nhánh tại Quận 3. Trụ sở chính là một tòa nhà 5 tầng gồm Data Center và các văn phòng làm việc dành cho CEO, HR, Project manager, Technical Manager, Business Analyst, IT manager và các nhóm developer và tester cho các project thuộc thị trường nước ngoài. Chi nhánh tại Quận 3 là văn phòng làm việc của các nhóm developer và tester cho các project thuộc thị trường trong nước

## Mục tiêu

Bài tập này giả định Công ty muốn thiết lập một hệ thống mạng cho trụ sở chính và chi nhánh với các yêu cầu sau: 

- Tại trụ sở chính 

    - Developer và Tester chỉ được sử dụng máy bàn tại công ty, không được sử dụng laptop riêng để truy cập vào mạng của công ty. 

    - CEO, HR, Project manager, Technical Manager, Business Analyst, IT manager được sử dụng Laptop, truy cập vào hệ thống wifi nội bộ sử dụng tài khoản xác thực. 

    - Một hệ thống wifi public với đường kết nối Internet riêng. 

    - Hệ thống phần cứng để triển khai hệ thống server ảo phục vụ cho việc deploy các ứng dụng trong giai đoạn test. 

    - Sử dụng các dịch vụ Cloud deploy các ứng dụng trong giai đoạn staging để khách hàng sử dụng thử trước khi đưa ra thực tế.

- Tại chi nhánh: 

    - Developer và Tester chỉ được sử dụng máy bàn tại công ty, không được sử dụng laptop riêng để truy cập vào mạng của công ty. 

    - Sử dụng kết nối VPN site-to-site để deploy ứng dụng lên hệ thống tại Data Center. 

    - Một hệ thống wifi với đường kết nối Internet riêng.

## Mô hình mạng

![](netdesign-final-3.png)

## Bảng chia subnet và VLAN

- Trụ sở (HQ)

| CIDR            | Range                         | Note               |
|-----------------|-------------------------------|--------------------|
| 100.1.1.0/30    | 100.1.1.0 - 100.1.1.3         | ISP - R1           |
| 100.2.2.0/30    | 100.2.2.0 - 100.2.2.3         | ISP - R2           |
| 192.168.1.0/29  | 192.168.1.0 - 192.168.1.7     | R1 - R2 - SERVERS  |
| 192.168.2.0/30  | 192.168.2.0 - 192.168.2.3     | R1 - MLS1          |
| 192.168.2.4/30  | 192.168.2.4 - 192.168.2.7     | R1 - MLS2          |
| 192.168.2.8/30  | 192.168.2.8 - 192.168.2.11    | R2 - MLS1          |
| 192.168.2.12/30 | 192.168.2.12 - 192.168.2.15   | R2 - MLS2          |
| 192.168.10.0/27 | 192.168.10.0 - 192.168.10.31  | VLAN10 - HR        |
| 192.168.20.0/27 | 192.168.20.0 - 192.168.20.31  | VLAN20 - BA        |
| 192.168.30.0/27 | 192.168.30.0 - 192.168.30.31  | VLAN30 - ITM       |
| 192.168.40.0/27 | 192.168.40.0 - 192.168.40.31  | VLAN40 - PM        |
| 192.168.50.0/27 | 192.168.50.0 - 192.168.50.31  | VLAN50 - TM        |
| 192.168.60.0/26 | 192.168.60.0 - 192.168.60.63  | VLAN60 - DEVELOPER |
| 192.168.70.0/26 | 192.168.70.0 - 192.168.70.63  | VLAN70 - TESTER    |
| 192.168.80.0/29 | 192.168.80.0 - 192.168.80.7   | VLAN80 - CEO       |
| 192.168.90.0/24 | 192.168.90.0 - 192.168.90.255 | VLAN90 - WIFI      |
| 172.168.0.0/23  | 172.168.0.0 - 172.168.1.255   | WIFI PUBLIC        |

- Chi nhánh (BR)

| CIDR             | Range                          | Note                |
|------------------|--------------------------------|---------------------|
| 100.3.3.0/30     | 100.3.3.0 - 100.3.3.3          | ISP - R3            |
| 100.4.4.0/30     | 100.4.4.0 - 100.4.4.3          | ISP - R4            |
| 192.168.1.0/30   | 192.168.1.0 - 192.168.1.3      | R3 - MLS1           |
| 192.168.1.4/30   | 192.168.1.4 - 192.168.1.7      | R3 - MLS2           |
| 192.168.1.8/30   | 192.168.1.8 - 192.168.1.11     | R4 - MLS1           |
| 192.168.1.12/30  | 192.168.1.12 - 192.168.1.15    | R4 - MLS2           |
| 192.168.100.0/27 | 192.168.100.0 - 192.168.100.63 | VLAN100 - DEVELOPER |
| 192.168.200.0/27 | 192.168.200.0 - 192.168.200.63 | VLAN200 - TESTER    |
| 172.168.2.0/24   | 172.168.2.0 - 172.168.2.255    | WIRELESS ROUTER AP  |

...

> **_Note_** : Chi tiết hơn tại [Drive](https://drive.google.com/drive/folders/1SbakLJsVqzZIdV6OYrDTCgL3D8dQYNtU)

## Thành viên

- Thuan Tong-Vo-Anh, [@thu4n](https://github.com/thu4n/)
- Vu Le-Huynh-Quang, [@r1anl3](https://github.com/r1anl3/)
- To Nguyen-Dang, [@Nyx](https://github.com/NguyenDangTo)