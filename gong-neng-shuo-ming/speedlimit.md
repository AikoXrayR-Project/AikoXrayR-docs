# Mô tả chức năng giới hạn tốc độ

1. Giới hạn tốc độ nút: Vui lòng điền vào giới hạn tốc độ nút của SSpanel, tính bằng Mbps.
2. Giới hạn tốc độ người dùng: Vui lòng điền vào cài đặt người dùng của SSpanel, đơn vị là Mbps.
3. Nếu giá trị giới hạn tốc độ được đặt thành 0, có nghĩa là không có giới hạn tốc độ.

## Cài đặt giới hạn tốc độ nút cục bộ

Đối với bảng không hỗ trợ cài đặt giới hạn tốc độ từ xa: chẳng hạn như V2board, giới hạn tốc độ có thể được đặt trong tệp cấu hình cục bộ `SpeedLimit`. Lưu ý rằng cài đặt này ghi đè giới hạn tốc độ cấp nút để tìm nạp từ xa.

{% hint style = "info"%}
Giới hạn tốc độ nút: Tất cả các giá trị giới hạn tốc độ của người dùng được kết nối với nút này sẽ sử dụng giá trị được đặt trong `SpeedLimit` ** (không phải giới hạn tốc độ cổng) **
{% endhint%}

Xem tệp cấu hình để biết chi tiết:[Mô tả tệp cấu hình](../xrayr-pei-zhi-wen-jian-shuo-ming/config.md#mian-ban-dui-jie-pei-zhi)

