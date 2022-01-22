# Mô tả chức năng xuất tùy chỉnh

XrayR hỗ trợ đầy đủ tất cả các chức năng xuất tùy chỉnh do Xray-core cung cấp. Các phương pháp kích hoạt cụ thể như sau:

1. Viết tệp \ _outbound.json tùy chỉnh, cấu hình này hoàn toàn giống với cấu hình gửi đi của Xray, vui lòng kiểm tra:[https://xtls.github.io/config/outbound.html](https://xtls.github.io/config/outbound.html)Được trợ giúp.
2. Định cấu hình `OutboundConfigPath` trong` config.yml` làm đường dẫn của custom \ _outbound.json.

### Ví dụ về chức năng xuất tùy chỉnh

```text
[
    {
        "tag": "IPv4_out",
        "protocol": "freedom"
    },
    {
        "tag": "IPv6_out",
        "protocol": "freedom",
        "settings": {
            "domainStrategy": "UseIPv6"
        }
    },
    {
        "protocol": "blackhole",
        "tag": "block"
    }
]
```

