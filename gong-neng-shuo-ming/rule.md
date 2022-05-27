# Mô tả chức năng kiểm tra

1. Vui lòng điền vào bất kỳ biểu thức chính quy nào trong quy tắc kiểm tra giao diện người dùng. Ví dụ: `baidu.com` sẽ chặn tất cả các tên miền baidu và` (. + \. | ^) (360 | so) \. (Cn | com) `sẽ chặn tất cả các tên miền baidu Chặn các trang web liên quan đến 360.
2. Hỗ trợ địa chỉ ip đầu vào để che ip, chẳng hạn như `127.0.0.1`.
3. Đối với che chắn giao thức BT, vui lòng kiểm tra:[Mô tả chức năng định tuyến tùy chỉnh](zi-ding-yi-lu-you-gong-neng-shuo-ming.md)

## Cài đặt quy tắc kiểm tra cục bộ

Đối với các bảng không hỗ trợ thiết lập từ xa các quy tắc kiểm tra: chẳng hạn như V2board, bạn có thể đặt đường dẫn tệp quy tắc cục bộ trong tệp cấu hình cục bộ `RuleListPath`. Tệp quy tắc không cần xác định loại tệp, mỗi ** quy tắc thông thường ** có một dòng và nhãn ID quy tắc cục bộ mặc định là -1.

Xem tệp cấu hình để biết chi tiết:[Mô tả tệp cấu hình](../config-AikoXrayR/config.md#mian-ban-dui-jie-pei-zhi)

**Tệp quy tắc cục bộ mẫu**

Hãy đảm bảo rằng mỗi dòng chỉ là một quy tắc thông thường đơn giản và không chứa bất kỳ chuỗi nào khác không liên quan.
```text
(.+\.|^)(360|so)\.(cn|com)
baidu.com
google.com
127.0.0.1
```

