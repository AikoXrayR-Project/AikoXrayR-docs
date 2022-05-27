# Cấu hình đế cắm cơ bản

1. Định cấu hình `PanelType:" V2board "` trong `config.yml`.
2. V2board chỉ hỗ trợ các quy tắc kiểm tra cho các loại nút V2ray.
3. Kích hoạt vless và xtls, vui lòng khởi động thủ công trong tệp cấu hình, V2board không hỗ trợ cấu hình trực tuyến.

Xem tệp cấu hình để biết chi tiết:[Mô tả tệp cấu hình](../config-AikoXrayR/config.md)

### Gắn kết vmess + grpc

Để hỗ trợ thành công kết nối sự cố, khi kết nối với vmess + grpc, v2board cần thêm nội dung sau vào cấu hình giao thức truyền:

```text
{
  "serviceName": "host",
}
```

，Trường hợp `" name "` được thay thế bằng tên miền của bạn hoặc tên miền giảm tải khác

### Gắn kết vmess + tcp + http

Khi kết nối với vmess + tcp + http, v2board cần thêm nội dung sau vào cấu hình giao thức truyền:

```text
{
  "header": {
    "type": "http",
    "request": {},
    "response": {}
  }
}
```

Vui lòng tham khảo nội dung của `yêu cầu` và` phản hồi ` [Tài liệu Xray-core](https://xtls.github.io/config/transports/tcp.html#httpheaderobject)cài đặt。

