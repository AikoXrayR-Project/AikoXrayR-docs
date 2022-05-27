# Kết nối Shadowsocks

| thỏa thuận | Hỗ trợ | Phương pháp mã hóa |
| :--- | :--- | :--- |
| ShadowsocksAEAD | √ | aes-128-gcm, aes-256-gcm, chacha20-ietf-poly1305 |

## SSpanel-uim nút địa chỉ định dạng

* Lưu ý rằng loại nút chọn: 'Shadowsocks'
* Một cổng đa người dùng lưu trữ mã hóa người dùng chọn: 'aes-128-gcm', 'aes-256-gcm', 'chacha20-ietf-poly1305'.
* XrayR hiện chỉ hỗ trợ một cổng duy nhất nhiều người dùng lưu trữ người dùng, nhiều hơn một người dùng lưu trữ chỉ sử dụng đầu tiên.

```text
  Tên miền hoặc IP; port= Cổng nghe #Cổng kết nối; server=xx
  ```

## Shadowsocks ví dụ

```text
Ví dụ: gz.aaa.com; port=80#1234; server=gz.aaa.com
```

