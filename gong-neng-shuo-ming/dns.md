# Mô tả DNS tùy chỉnh

XrayR hỗ trợ thiết lập các chính sách DNS khác nhau cho các nút khác nhau. Các phương pháp cụ thể như sau:

1. Viết tệp dns.json, cấu hình này hoàn toàn giống với cấu hình DNS Xray, vui lòng kiểm tra:[https://xtls.github.io/config/dns.html](https://xtls.github.io/config/dns.html) 获取帮助。
2. Định cấu hình `DnsConfigPath` trong` config.yml` làm đường dẫn của dns.json.
3. Đặt `EnableDNS` thành true trên nút cần bật DNS tùy chỉnh. Nếu được đặt thành false hoặc không được điền, DNS cục bộ sẽ được sử dụng.
4. Nếu bạn muốn bật cấu hình liên quan đến geoip, hãy đảm bảo rằng `geoip.dat` và` geosite.dat` nằm trong cùng một thư mục với `config.yml`.

## Cấu hình mẫu mở khóa DNS

```javascript
{
    "servers": [
      "8.8.8.8", 
      {
        "address": "1.1.2.2", // 购买的 DNS 解锁提供的 IP
        "port": 53,
        "domains": [
          "geosite:netflix" 
        ]
      }
    ]
  }
```

## Đặt mức độ ưu tiên IPV6

1. Vui lòng đảm bảo máy chủ lưu trữ có địa chỉ ipv6 trước, nếu không, vui lòng xem xét sử dụng[warp](https://github.com/P3TERX/warp.sh)lấy ipv6。
2. Đặt `EnableDNS` thành true trên nút cần đặt mức ưu tiên IPV6.
3. Đặt `SendIP` thành` "::" `trên nút cần đặt ưu tiên IPV6.
4. Đặt `DNSType` thành` UseIP` trong nút cần đặt mức ưu tiên IPV6.

Cho đến nay, XrayR sẽ ưu tiên sử dụng địa chỉ ipv6 của trang web đích để truy cập, điều này sẽ không ảnh hưởng đến quyền truy cập của trang ipv4 mặc định. ~~ Có thể được sử dụng để bỏ chặn Netflix và các nhu cầu khác ~~

## Đặt mức độ ưu tiên IPV4

1. Đặt `EnableDNS` thành true trên nút cần đặt ưu tiên IPV4.
2. Đặt `SendIP` thành` "0.0.0.0" `trong nút cần đặt mức ưu tiên IPV4.
3. Đặt `DNSType` thành` UseIP` trên nút cần đặt mức ưu tiên IPV4.

