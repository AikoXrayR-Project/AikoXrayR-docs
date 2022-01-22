# Mô tả chức năng định tuyến tùy chỉnh

XrayR hỗ trợ đầy đủ tất cả các chức năng định tuyến tùy chỉnh do Xray-core cung cấp. Các phương pháp kích hoạt cụ thể như sau:

1. Viết tệp route.json, cấu hình này hoàn toàn giống với cấu hình định tuyến Xray, vui lòng kiểm tra:[https://xtls.github.io/config/routing.html](https://xtls.github.io/config/routing.html)Được trợ giúp.
2. Định cấu hình `RouteConfigPath` làm đường dẫn của route.json trong` config.yml`.
3. Nếu bạn muốn bật cấu hình liên quan đến geoip, hãy đảm bảo rằng `geoip.dat` và` geosite.dat` nằm trong cùng một thư mục với `config.yml`.
{% hint style = "info"%}
InboundTag / outboundTag được tạo tự động của một nút được lấy từ xa có dạng NodeType \ _Port. Chẳng hạn như: V2ray \ _80. Các thẻ gửi đến / gửi đi đều giống nhau.
{% endhint%}

### Ví dụ về chức năng định tuyến tùy chỉnh

```text
{
    "domainStrategy": "IPOnDemand",
    "rules": [
        {
            "type": "field",
            "outboundTag": "block",
            "ip": [
                "geoip:private"
            ]
        },
        {
            "type": "field",
            "outboundTag": "block",
            "protocol": [
                "bittorrent"
            ]
        },
        {
            "type": "field",
            "outboundTag": "IPv6_out",
            "domain": [
                "geosite:netflix"
            ]
        }
    ]
}
```

