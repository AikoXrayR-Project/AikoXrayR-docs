# Liên quan đến tối ưu hóa bộ nhớ

## Tối ưu hóa kiểm soát liên kết

Được phát hành bởi kết nối `ConnectionConfig` tùy chỉnh[Cấu hình liên quan](../config-AikoXrayR/config.md#lian-jie-kong-zhi)，Có thể tối ưu hóa việc sử dụng bộ nhớ ở một mức độ nhất định

1. Giảm `ConnIdle` có thể tối ưu hóa việc sử dụng bộ nhớ khi số lượng kết nối nhiều, nhưng nó sẽ dẫn đến độ trễ kết nối của người dùng cao hơn.
2. Trong kịch bản duyệt HTTP, có thể đặt `UplinkOnly` và` DownlinkOnly` thành 0 để cải thiện hiệu quả của việc đóng kết nối và giảm mức sử dụng bộ nhớ.
3. Giảm `BufferSize` có thể tối ưu hóa việc sử dụng bộ nhớ, nhưng có thể làm tăng mức sử dụng CPU.
