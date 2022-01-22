---
Mô tả: Một khung phụ trợ Xray có thể dễ dàng hỗ trợ nhiều bảng.
---

# Về XrayR

## XrayR

Một khung phụ trợ Xray có thể dễ dàng hỗ trợ nhiều bảng.

Một khung công tác back-end dựa trên Xray, hỗ trợ các giao thức V2ay, Trojan, Shadowsocks, cực kỳ dễ mở rộng và hỗ trợ kết nối nhiều bảng điều khiển.


## thư mục dự án

* [XrayR](https://github.com/herotbty/XrayR)：Mã nguồn XrayR và phân phối phần mềm.
* [XrayR-release](https://github.com/herotbty/XrayR-release)：Tập lệnh cài đặt một cú nhấp chuột của XrayR cùng với Docker.
* [XrayR-doc](https://github.com/herotbty/XrayR-doc)：Mã nguồn tài liệu XrayR.

## Đặc trưng

* Mã nguồn mở vĩnh viễn và miễn phí.
* Hỗ trợ nhiều giao thức V2ray, Trojan, Shadowsocks.
* Hỗ trợ các tính năng mới như Vless và XTLS.
* Hỗ trợ kết nối đơn lẻ với nhiều bảng và nút mà không cần khởi động lại.
* Hỗ trợ IP trực tuyến bị hạn chế
* Hỗ trợ mức cổng nút, giới hạn tốc độ mức người dùng.
* Cấu hình đơn giản và rõ ràng.
* Sửa đổi cấu hình để tự động khởi động lại phiên bản.
* Dễ dàng biên dịch và nâng cấp, có thể nhanh chóng cập nhật phiên bản lõi, hỗ trợ các tính năng mới của Xray-core.

## Đặc trưng

| Đặc trưng                         | v2ray | trojan | shadowsocks |
| ---------------------------       | ----- | ------ | ----------- |
| Nhận thông tin về nút             | √     | √      | √           |
| Nhận thông tin người dùng         | √     | √      | √           |
| Thống kê lưu lượng người dùng     | √     | √      | √           |
| Báo cáo thông tin máy chủ         | √     | √      | √           |
| Tự động đăng ký chứng chỉ TLS     | √     | √      | √           |
| tự động gia hạn chứng chỉ tls     | √     | √      | √           |
| Số người trực tuyến               | √     | √      | √           |
| Hạn chế Người dùng Trực tuyến     | √     | √      | √           |
| quy tắc kiểm toán                 | √     | √      | √           |
| Giới hạn tốc độ cổng nút          | √     | √      | √           |
| Giới hạn tốc độ của người dùng    | √     | √      | √           |
| DNS tùy chỉnh                     | √     | √      | √           |
## Hỗ trợ giao diện người dùng

| đầu trước                                              | v2ray | trojan | shadowsocks                                 |
| ------------------------------------------------------ | ----- | ------ | ------------------------------------------- |
| [sspanel-uim](https://github.com/Anankke/SSPanel-Uim)  | √     | √      | √ (Đa người dùng một cổng và V2ray-Plugin)  |
| [v2board](https://github.com/v2board/v2board)          | √     | √      | √                                           |
| [PMPanel](https://github.com/ByteInternetHK/PMPanel)   | √     | √      | √                                           |
| [ProxyPanel](https://github.com/ProxyPanel/ProxyPanel) | √     | √      | ×                                           |

## Giao thức hỗ trợ V2ray

| giao thức      | Tình hình hỗ trợ                                                                    |
| :--------      | :---------------------------------------------------------------------------------- |
| VMess          | tcp, tcp+http, tcp+tls, ws, ws+tls, h2c, h2+tls, grpc, grpc+tls                     |
| VMessAEAD      | tcp, tcp+http, tcp+tls, ws, ws+tls, h2c, h2+tls, grpc, grpc+tls                     |
| VLess          | tcp, tcp+http, tcp+tls/xtls, ws, ws+tls/xtls, h2c, h2+tls/xtls, grpc, grpc+tls/xtls |

## Thỏa thuận hỗ trợ Trojan

| giao thức  | Tình hình hỗ trợ |
| :-----     | :-------         |
| Trojan     | √                |

## Giao thức hỗ trợ Shadowsocks

| giao thức          | Tình hình hỗ trợ | phương pháp mã hóa                               |
| :----------------- | :--------------- | :----------------------------------------------- |
| ShadowsocksAEAD    | √                | aes-128-gcm, aes-256-gcm, chacha20-ietf-poly1305 |

