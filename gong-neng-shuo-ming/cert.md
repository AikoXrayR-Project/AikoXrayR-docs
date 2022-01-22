# Hướng dẫn đăng ký chứng chỉ tự động

XrayR hỗ trợ nhiều cấu hình yêu cầu chứng chỉ tự động. Chứng chỉ được áp dụng sẽ được đặt trong thư mục `cert` trong thư mục**config file \ (config.yml \)**.

Sau đây là các mô tả tệp cấu hình có liên quan để tự động đăng ký chứng chỉ.

```yaml
CertConfig:
    CertMode: dns # Option about how to get certificate: none, file, http, dns. Choose "none" will forcedly disable the tls config.
    CertDomain: "node2.test.com" # Domain to cert
    CertFile: /etc/XrayR/cert/node2.test.com.cert # Provided if the CertMode is file
    KeyFile: /etc/XrayR/cert/node2.test.com.key
    Provider: alidns # DNS cert provider, Get the full support list here: https://go-acme.github.io/lego/dns/
    Email: test@me.com
    DNSEnv: # DNS ENV option used by DNS provider
        ALICLOUD_ACCESS_KEY: aaa
        ALICLOUD_SECRET_KEY: bbb
```

| tham số | 选项 | 说明 |
| :--- | :--- | :--- |
| `CertMode` | `none`,`file`,`http`,`dns` | 获Làm thế nào để nhận được chứng chỉ. `tệp`: Cung cấp thủ công và chỉ định đường dẫn. `http`: Đăng ký qua http, yêu cầu cổng 80. `dns`: Để sử dụng chế độ dns, bạn cần phải xây dựng cấu hình của nhà cung cấp dịch vụ dns có liên quan. `none`: Buộc đóng cài đặt tls và để nginx hoặc caddy xử lý.|
| `CertDomain` | Không  | Đăng ký tên miền chứng chỉ|
| `CertFile` | Không  | Đường dẫn chứng chỉ được chỉ định theo cách thủ công |
| `KeyFile` | Không  | Đường dẫn khóa cá nhân được chỉ định theo cách thủ công |
| `Provider` | Không  |Các nhà cung cấp dns, tất cả các nhà cung cấp dns được hỗ trợ có thể được tìm thấy tại đây:[https://go-acme.github.io/lego/dns/](https://go-acme.github.io/lego/dns/) |
| `DNSEnv` | Không  |Đối với các biến môi trường bắt buộc để đăng ký chứng chỉ sử dụng DNS, vui lòng tham khảo liên kết ở trên và điền vào các thông số do nhà cung cấp DNS của riêng bạn yêu cầu. Hãy chú ý đến một dòng trên mỗi dòng và nó phải tuân theo định dạng tệp yaml khi điền vào. |

