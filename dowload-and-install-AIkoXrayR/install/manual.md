# Hướng dẫn cài đặt

## Tải xuống và sử dụng

1. Tại đây, chọn phiên bản phù hợp theo hệ thống của bạn:[Release](https://github.com/AikoXrayR-project/XrayR/releases)
2. Giải nén kho lưu trữ và chạy:`./XrayR -config config.yml`

## biên dịch và sử dụng

1. go 1.18.1
2. chạy tuần tự

   ```bash
   git clone https://github.com/AikoXrayR-project/XrayR
   cd XrayR/main
   go mod tidy
   go build -o XrayR -ldflags "-s -w"
   ./XrayR -config config.yml
   ```

Xem tệp cấu hình để biết chi tiết:[Mô tả tệp cấu hình](../../config-AikoXrayR/config.md)

