# Gắn kết với V2ray

| giao thức| Tình hình hỗ trợ |
| :--- | :--- |
| VMess | tcp, tcp+http, tcp+tls, ws, ws+tls, h2c, h2+tls, grpc, grpc+tls |
| VMessAEAD | tcp, tcp+http, tcp+tls, ws, ws+tls, h2c, h2+tls, grpc, grpc+tls |
| VLess | tcp, tcp+http, tcp+tls/xtls, ws, ws+tls/xtls, h2c, h2+tls/xtls, grpc, grpc+tls/xtls |

## SSpanel-uim nút địa chỉ định dạng

```text
IP; Cổng nghe; alterId;(tcp hoặcws) ;(tls hoặc không điền); path=/xxx|host=xxxx.com|server=xxx.com|outside_port=xxx
```

AlterId được đặt thành 0 và VMessAEAD sẽ được kích hoạt tự động.

{% hint style="info" %} Lưu ý: VMESS AEAD sẽ bắt buộc bật vào ngày 1 tháng 1 năm 2022 Xin lưu ý cập nhật cấu hình phía dịch vụ, thiết lập alterId = 0 {% endhint %}

## tcp ví dụ

```text
ip; 12345;0; tcp;; server=tên miền
```

```text
Ví dụ: 1.3.5.7; 12345;0; tcp;; server=hk.domain.com
```

## tcp+http ví dụ

Lưu ý rằng sspanel không hỗ trợ việc phát hành các đăng ký như vậy, tùy chọn này chỉ dành cho sự nhầm lẫn http bật bật.

```text
ip; 12345;0; tcp;; server=tên miền; headertype=http
```

```text
Ví dụ: 1.3.5.7; 12345;0; tcp;; server=hk.domain.com; headertype=http
```

## tcp + tls Ví dụ

```text
ip;12345;0;tcp;tls; server=tên miền|host=tên miền
```

```text
Ví dụ：1.3.5.7;12345;0;tcp;tls;server=hk.domain.com|host=hk.domain.com
```

## ws Ví dụ

```text
ip;80;0;ws;;path=/xxx|server=tên miền|host=CDN tên miền
```

```text
Ví dụ：1.3.5.7;80;0;ws;;path=/v2ray|server=hk.domain.com|host=hk.domain.com
```

## ws + tls Ví dụ

```text
ip;443;0;ws;tls;path=/xxx|server=tên miền|host=CDN tên miền
```

```text
Ví dụ：1.3.5.7;443;0;ws;tls;path=/v2ray|server=hk.domain.com|host=hk.domain.com
```

## ws + tls (Caddy/Nginx) ví dụ

Cấu hình nút TLS xử lý Caddy hoặc Nginx phù hợp với ws +tls, cấu hình 'CertMode: none' ở back-end

Đồng thời thiết lập outside_port là cổng nghe Caddy/Nginx, chuyển tiếp đến 12345 cho cổng nghe XrayR. Bạn có thể cấu hình 'ListenIP: 127.0.0.1' để nghe cổng cục bộ.

```text
ip;12345;0;tls;ws;path=/xxx|server=域名|host=CDN域名|outside_port=443
```

```text
Ví dụ: 1. 3。 5。 7; 12345;0; Wise; Turs; Parth =/v2ray| Sever = Huck. Doman. Comm| Horst Huck. Doman. Ví dụ com: 1. 3。 5。 7; 12345; 2; Wise; Turs; Parth =/vi2 thuận| Sever = Huck. Doman. Comm| Horst Huck. Doman. Comm
```

## grpc+tls ví dụ

Sử dụng grpc khuyến nghị nâng cấp sspanel đến [Anankke/SSPanel-Uim@8f68b63] (https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107)

```text
ip; 12345;0; grpc; tls; host=tên miền|server=tên miền|servicename=tên miền
```

```text
Ví dụ: 1.3.5.7; 12345;0; grpc; tls; host=hk.domain.com|server=hk.domain.com|servicename=hk.domain.com
```

## Cổng quá cảnh

Thêm '|outside_port = xxx' sau khi bất kỳ nhóm cấu hình  | hợp nào, một cổng kết nối người dùng.

XrayR không có tùy chọn cấu hình 'inside_port =xx', và để nghe cổng cục bộ, hãy đặt ip nghe trong hồ sơ là '127.0.0.1'.

```text
Ví dụ: 1.3.5.7; 80;0; ws;; path=/v2ray|server=hk.domain.com|host=hk.domain.com|outside_port=12345
```

## Bật Vless

Đây là một tính năng thử nghiệm, đảm bảo rằng bảng điều khiển bạn đang sử dụng đã hỗ trợ đăng ký vless, nếu không cấu hình máy khách theo cách thủ công. 
sspanel nâng cấp lên phiên bản này [Anankke/SSPanel-Uim@8f68b63] (https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107) hỗ trợ đăng ký vless

Thêm 'enable_vless = true sau khi cấu hình giao thức tùy ý`

```text
Ví dụ: hk.domain.com; 12345;0; tcp;(tls hoặc xtls); server=hk.domain.com|enable_vless=true
```

Đồng thời thiết lập các tập tin tại địa phương đặt 'EnableVless' như true. Hồ sơ được nêu chi tiết: [Mô tả hồ sơ] (.. /.. /xrayr-pei-zhi-wen-jian-shuo-ming/config.md#mian-ban-dui-jie-pei-zhi)

Vui lòng bật vless và luôn luôn sử dụng tls hoặc xtls.

## Cho phép xtls

Đây là một tính năng thử nghiệm, đảm bảo rằng bảng điều khiển bạn đang sử dụng đã hỗ trợ đăng ký với xtls, nếu không cấu hình máy khách theo cách thủ công. 
sspanel nâng cấp lên phiên bản này [Anankke/SSPanel-Uim@8f68b63] (https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107) hỗ trợ đăng ký xtls

Thay thế 'tls' trong bất kỳ cấu hình giao thức nào bằng 'xtls', nếu xtls có flow điều khiển luồng, nó sẽ được thêm vào cuối: '|flow = flow-vlaue'

```text
Ví dụ: hk.domain.com; 443;0; tcp; xtls; server=hk.domain.com|host=hk.domain.com|enable_vless=true|flow=xtls-rprx-direct
```

Các tập tin được thiết lập tại địa phương đặt 'EnableXTLS' thành true. Hồ sơ được nêu chi tiết: [Mô tả hồ sơ] (.. /.. /xrayr-pei-zhi-wen-jian-shuo-ming/config.md#mian-ban-dui-jie-pei-zhi)

