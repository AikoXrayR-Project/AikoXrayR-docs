# Mô tả chức năng dự phòng

> Dự phòng cung cấp cho Xray khả năng phát hiện chống tích cực cường độ cao và có cơ chế dự phòng gói đầu tiên ban đầu.
>
> Dự phòng cũng có thể phân chia các loại lưu lượng khác nhau theo đường dẫn, để nhận ra một cổng và nhiều dịch vụ chia sẻ.
>
> Hiện tại, bạn có thể sử dụng tính năng dự phòng bằng cách định cấu hình các dự phòng khi sử dụng giao thức VLESS hoặc trojan, đồng thời tạo ra sự kết hợp rất phong phú của trò chơi.
>
> ---[https://xtls.github.io/config/features/fallback.html](https://xtls.github.io/config/features/fallback.html)

## Bật chức năng Dự phòng

Đặt `EnableFallback` thành` true` và định cấu hình `FallBackConfigs`

```yaml
ControllerConfig:
  EnableFallback: true # Only support for Trojan and Vless
  FallBackConfigs:  # Support multiple fallbacks
    -
      SNI: # TLS SNI(Server Name Indication), Empty for any
      Path: # HTTP PATH, Empty for any
      Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/fallback/ for details.
      ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for dsable
```
## Định cấu hình Dự phòng

XrayR tuân theo ý tưởng thiết kế Xray và hỗ trợ nhiều cài đặt Dự phòng cho một nút, vì vậy `FallBackConfigs` là một mảng và ví dụ về mỗi phần tử con như sau:

```yaml
-
  SNI: # TLS SNI(Server Name Indication), Empty for any
  Path: # HTTP PATH, Empty for any
  Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/fallback/ for details.
  ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for dsable
```

### SNI: chuỗi

Cố gắng khớp TLS SNI \ (Chỉ báo tên máy chủ \), trống là bất kỳ, mặc định là ""

### Đường dẫn: chuỗi

Cố gắng khớp với HTTP PATH của gói đầu tiên, trống là tùy ý, mặc định là trống, không trống phải bắt đầu bằng "/", h2c không được hỗ trợ.

Thông minh: VLESS sẽ cố gắng xem xét PATH khi cần thiết (không quá 55 byte; thuật toán nhanh nhất, không phân tích cú pháp hoàn toàn HTTP) và nếu thành công, xuất thông tin realPath = vào nhật ký. Mục đích: Chuyển hướng lưu lượng truy cập WebSocket gửi đến khác hoặc lưu lượng giả mạo HTTP, không xử lý dư thừa, lưu lượng chuyển tiếp thuần túy và phép đo thực tế mạnh hơn thế hệ ngược Nginx.

Lưu ý: Đầu vào nơi đặt dự phòng phải là TCP + TLS, được sử dụng để giảm tải cho WS gửi đến khác. Không cần định cấu hình TLS cho đầu vào đã được giảm tải.

### Dest: string \ | number

Xác định đích của lưu lượng TCP sau khi giải mã TLS. Hiện tại, hai loại địa chỉ được hỗ trợ: (Mục này là bắt buộc, nếu không, không thể khởi động mục này)

1. TCP, định dạng là "addr: port", trong đó addr hỗ trợ IPv4, tên miền và IPv6. Nếu bạn điền tên miền, kết nối TCP sẽ được khởi tạo trực tiếp (không sử dụng DNS tích hợp).
2. Unix miền socket, định dạng là một đường dẫn tuyệt đối, chẳng hạn như "/dev/shm/domain.socket", bạn có thể thêm "@" ở đầu để biểu thị trừu tượng và "@@" để biểu thị trừu tượng với đệm.

   Nếu bạn chỉ điền vào cổng, các số hoặc chuỗi có thể được sử dụng, chẳng hạn như 80, "80", thường trỏ đến dịch vụ http bản rõ (addr sẽ được bổ sung bằng "127.0.0.1").

### ProxyProtocolVer: số

Gửi giao thức PROXY, dành riêng để chuyển IP nguồn thực và cổng của yêu cầu, điền vào phiên bản 1 hoặc 2, mặc định là 0, nghĩa là không được gửi. Điền vào 1 nếu cần thiết.

Hiện tại điền 1 hoặc 2, chức năng hoàn toàn giống nhau, nhưng cấu trúc khác nhau, và cái trước có thể được in ra, cái sau là nhị phân. Cả TCP và WS đầu vào của Xray đều đã hỗ trợ nhận giao thức PROXY.

> MẸO
>
> Nếu bạn đang định cấu hình Nginx để nhận giao thức PROXY, ngoài việc đặt proxy \ _protocol, bạn cũng cần đặt set \ _real \ _ip \ _from, nếu không có thể xảy ra sự cố.

## Ví dụ về dự phòng

Cài đặt XrayR
```text
EnableFallback: true
FallBackConfigs:  # Support multiple fallbacks
  -
    SNI:
    Path:
    Dest: 8080
    ProxyProtocolVer: 0
```

Cài đặt Nginx

```text
server {  
    listen 8080 http2;
  root /var/www/public; # 改成你自己的路径
  index index.php index.html;
  server_name www.test.com; # 改成你自己的域名

  location / {
    try_files $uri /index.php$is_args$args;
  }

  location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass 127.0.0.1:9000; # unix:/run/php/php-fpm.sock;
  }
}
```

## tham khảo

[Xray Fallback](https://xtls.github.io/config/features/fallback.html)

