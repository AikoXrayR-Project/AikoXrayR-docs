# Tại sao giới thiệu Shadowsocks - V2Ray-Plugin

## Cập nhật vào 2021/07/04

Tôi đã đổ lỗi nhầm cho Trojan. Việc vô hiệu hóa TLS thông qua phần phụ trợ cũng có thể đạt được với mô-đun Luồng của Nginx. Proxy Nginx xử lý TLS của Trojan để đạt được hiệu quả ẩn thông tin bắt tay TLS và đồng thời, nó có thể dự phòng cho các trang web http1.1 để đạt được cao hơn cấp hiệu suất SS.

## Nguyên bản

Nhiều người nghĩ rằng chỉ một cổng Shadowsocks là đủ, tại sao lại giới thiệu Shadowsocks - V2Ray-Plugin?

Trước hết, theo tình hình giao tiếp Internet quốc tế gần đây, phân tích cá nhân của tôi tin rằng trong những giai đoạn đặc biệt, hành vi bắt tay TLS của go sẽ bị khớp và bị chặn. Ngoài ra, hầu hết các phần mềm hiện có (chẳng hạn như V2ray-core, Xray-core) đều được triển khai khi chạy và sử dụng thư viện go để xử lý TLS. Do đó, trong một khoảng thời gian đặc biệt, hành vi bắt tay của TLS khi di chuyển có thể được xác định, dẫn đến việc chặn cổng chính xác. Do đó, hầu hết các giao thức sử dụng trực tiếp để xử lý TLS, chẳng hạn như Trojan, đã bị chặn nghiêm trọng trong những ngày gần đây. Tương tự như vậy, giả mạo bằng cách sử dụng Caddy đã bị chặn.

Mặc dù hành vi xác định thư viện TLS cho go có tỷ lệ dương tính giả rất lớn (chặn trang web chống tạo Caddy thông thường), nhưng nó đã được chứng minh là có thể xảy ra trong một giai đoạn đặc biệt. Theo tôi, cần ẩn hành vi bắt tay TLS của go để đạt được khả năng tàng hình cao hơn. Đối với điều này, tôi nghĩ NGINX được viết bằng C là lựa chọn tốt nhất ngay bây giờ. Tình hình hiện có cũng cho thấy Vmess + ws + tls + nginx có khả năng sống sót tốt nhất hiện tại.

Mặc dù Vmess + ws + tls + nginx đã ẩn thành công thông tin bắt tay TLS của go, giao thức Vmess sẽ tạo ra nhiều mức sử dụng bộ nhớ do thiết kế riêng của nó. Đồng thời, thiết kế xác minh dựa trên thời gian của nó làm tăng độ khó khi sử dụng. ~~ Và Trojan tạm thời không hỗ trợ việc sử dụng các phần mềm khác để xử lý TLS ~~. Lúc này Shadowsocks - V2Ray-Plugin trở thành sự lựa chọn tốt nhất.

Shadowsocks - V2Ray-Plugin, lần đầu tiên dựa trên Shadowsocks. Nhờ thiết kế giao thức Shadowsocks, Shadowsocks có tốc độ nhanh hơn và xác minh không phụ thuộc vào thời gian so với Vmess. Đồng thời, V2Ray-Plugin cung cấp cho Shadowsocks khả năng thực hiện mã hóa websocket và mã hóa TLS. Nó tăng cường đáng kể tính bảo mật của Shadowsocks, do đó lưu lượng truy cập có thể được truyền trực tiếp trên mạng công cộng mà không cần đào hầm. Đồng thời, TLS có thể được chuyển giao cho NGINX để ẩn các tính năng liên quan của go và ngăn chặn các cổng bị chặn.

Tóm lại, để ẩn các tính năng, tôi thực sự khuyên bạn nên sử dụng cách tiếp cận nginx + ws + tls + everything.Trong tình hình hiện tại, cấu hình nginx + ws + tls + ss tốt hơn nginx + ws + tls + vmess . Đồng thời, để xem xét lâu dài, tôi khuyên tất cả phần mềm triển khai giao thức sử dụng thư viện TLS được cung cấp bởi ngôn ngữ C để xử lý liên quan đến TLS hoặc tham khảo Shadowsocks để tách lớp trình cắm thêm để tạo điều kiện sử dụng thứ ba- phần mềm của bên như nginx để xử lý TLS.
