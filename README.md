# Hướng dẫn cài đặt MySQL và phpMyAdmin trên Docker

MySQL Community Edition là phiên bản có thể tải xuống miễn phí của cơ sở dữ liệu nguồn mở phổ biến nhất thế giới. Dựa theo giấy phép GPL và được hỗ trợ bởi một cộng đồng các nhà phát triển mã nguồn mở.

PhpMyAdmin là một công cụ phần mềm miễn phí viết bằng ngôn ngữ PHP nhằm cung cấp một giao diện để quản lý cơ sở dữ liệu MySQL hoặc MariaDB.

Docker là một nền tảng phần mềm được thiết kế để giúp tạo, triển khai và chạy các ứng dụng dễ dàng hơn.

Đầu tiên cúng ta sẽ tạo một Docker Network với tên sql nhằm mục đích khởi chạy Docker Container MySQL và phpMyAdmin trong network này.

```
docker network create sql
```

Thực hiện lần lượt các lệnh sau đây sẽ khởi tạo MySQL Container trên Docker. Trước tiên, hãy tạo một thư mục dùng để lưu dữ liệu rồi sau đó chạy lệnh khởi tạo MySQL Container:

```
# Khởi tạo thư mục chứa dữ liệu mkdir -p /opt/mysql 
# Khởi tạo MySQL container docker run -d --name mysql --network sql -e MYSQL_ROOT_PASSWORD="12345" -v /opt/mysql:/var/lib/mysql -p 3306:3306 mysql:8.0.21
```

Thực hiện lần lượt các lệnh sau đây sẽ khởi tạo phpMyAdmin Container trên Docker. Để phpMyAdmin  có thể hoạt động chúng ta cần phải liên kết đến vùng chứa MySQL để phpMyAdmin có thể kết nối và truy cập cơ sở dữ liệu.

```
# Khởi tạo phpMyAdmin container docker run -d --name phpmyadmin --network sql -e PMA_HOST=sql -p 8080:80 phpmyadmin/phpmyadmin
```

Sau khi hoàn thành cài đặt MySQL và phpMyAdmin trên Docker, chúng ta truy cập địa chỉ dạng http://my-ip:8080/ như sau:

![Hướng dẫn cài đặt MySQL và phpMyAdmin trên Docker](https://techfinally.com/wp-content/uploads/2020/08/techfinally-huong-dan-cai-dat-mysql-va-phpmyadmin-tren-docker-h01-1024x544.jpg)

Bạn đăng nhập với thông tin tài khoản mặc định là root và mật khẩu như đã tạo ở trên.

![Hướng dẫn cài đặt MySQL và phpMyAdmin trên Docker](https://techfinally.com/wp-content/uploads/2020/08/techfinally-huong-dan-cai-dat-mysql-va-phpmyadmin-tren-docker-h02-1024x544.jpg)

Nguồn: [Hướng dẫn cài đặt MySQL và phpMyAdmin trên Docker](https://techfinally.com/huong-dan-cai-dat-mysql-va-phpmyadmin-tren-docker/)
