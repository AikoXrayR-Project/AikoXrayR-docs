# Kết nối Shadowsocks - V2Ray-Plugin

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x534F;&#x8BAE;</th>
      <th style="text-align:left">&#x52A0;&#x5BC6;&#x65B9;&#x6CD5;</th>
      <th style="text-align:left">&#x6DF7;&#x6DC6;&#x65B9;&#x6CD5;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Shadowsocks - V2Ray-Plugin</td>
      <td style="text-align:left">aes-128-gcm, aes-256-gcm, chacha20-ietf-poly1305</td>
      <td style="text-align:left">
        <p>simple_obfs_http,simple_obfs_tls,</p>
        <p>ws,ws+tls</p>
      </td>
    </tr>
  </tbody>
</table>

## SSpanel-uim nút địa chỉ định dạng

```text
IP; Cổng nghe; ;(ws hoặc obfs) ;(tls hoặc không điền); path=/xxx|host=xxxx.com|server=xxx.com|outside_port=xxx
```

Lưu ý rằng có hai dấu chấm phẩy đằng sau cổng nghe

## SSpanel-uim mã sửa đổi

Mã của SSpanel-uim về Shadowsocks - V2Ray-Plugin có một số vấn đề cần được sửa đổi để đăng ký chính xác.

Phương pháp này được viết trong [SSPanel-Uim@822d3c] (https://github.com/Anankke/SSPanel-Uim/commit/822d3cbcb3ad8f7e11874a96f05d73e5b016c164) và không đảm bảo rằng tiếp theo vẫn có hiệu lực。

### Sửa đổi phương pháp

Mở tệp .php srcModelsNode, tìm dòng 420 và chú thích nó.

Trước khi sửa đổi:

```text
$return_array['path'] = ($return_array['path'] . '?redirect=' . $user->getMuMd5());
```

Sau khi sửa đổi:

```text
$return_array['path'] = ($return_array['path'] . '?redirect=' . $user->getMuMd5());
```

## SSpanel-uim đăng ký

SSpanel-uim khuyến nghị Android, WIN và Mac sử dụngClash, IOS sử dụng Shadowrocket để có được đăng ký có chứa Shadowsocks - V2Ray-Plugin.

## ws + tls (Nginx) ví dụ (**khuyến nghị**)

Cấu hình nút TLS xử lý Caddy hoặc Nginx phù hợp với ws +tls, cấu hình 'CertMode: none' ở back-end

Đồng thời thiết lập outside_port là cổng nghe Ngnx, chuyển tiếp đến 12345 cho cổng nghe XrayR. Bạn có thể cấu hình 'ListenIP: 127.0.0.1' để nghe cổng cục bộ.

```text
ip; 12345;; ws; tls; path=/xxx|server=tên miền|host=CDN|outside_port =443
```

```text
Ví dụ: 1.3.5.7; 12345;; ws; tls; path=/ss|server=hk.domain.com|host=hk.domain.com|outside_port=443
```

## ws+tls Ví dụ

```text
ip;12345;;ws;tls;path=/xxx|host=xxxx.com|server=xxx.com
```

```text
Ví dụ：1.3.5.7;12345;;ws;tls;path=/ss|host=hk.domain.com|server=hk.domain.com
```

## ws Ví dụ

```text
ip;12345;;ws;;path=/xxx|host=xxxx.com|server=xxx.com
```

```text
Ví dụ：1.3.5.7;12345;;ws;;path=/ss|host=hk.domain.com|server=hk.domain.com
```

## simple\_obfs\_http Ví dụ

```text
ip;12345;;obfs;http;server=xxx.com
```

```text
Ví dụ：1.3.5.7;12345;;obfs;http;server=hk.domain.com
```

## simple\_obfs\_tls Ví dụ 
```text
ip;12345;;obfs;tls;server=xxx.com
```

```text
Ví dụ：1.3.5.7;12345;;obfs;tls;server=hk.domain.com
```

## Cổng quá cảnh

Thêm '|outside_port = xxx' sau khi bất kỳ kết hợp cấu hình nào được thêm vào, một cổng kết nối cho người dùng.

XrayR không có tùy chọn cấu hình 'inside_port =xx', và để nghe cổng cục bộ, hãy đặt ip nghe trong hồ sơ là '127.0.0.1'.

```text
Ví dụ: 1.3.5.7; 12345;; ws; tls; path=/ss|server=hk.domain.com|host=hk.domain.com|outside_port=8888
```

