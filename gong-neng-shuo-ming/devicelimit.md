# Mô tả chức năng hạn chế kết nối thiết bị

Vì một số lượng lớn bảng không còn hỗ trợ đặc điểm kỹ thuật giới hạn thiết bị từ xa, thông số giới hạn thiết bị cục bộ hiện đã được thêm vào.

Để bật tính năng này, hãy đặt `DeviceLimit` thành giá trị khác 0 trong tệp cấu hình. Lưu ý rằng cài đặt này sẽ ghi đè giới hạn về số lượng thiết bị người dùng có được từ xa.

Xem tệp cấu hình để biết chi tiết:[Mô tả tệp cấu hình](../config-AikoXrayR/config.md#mian-ban-dui-jie-pei-zhi)

## 全局设备限制

Khi phiên bản XrayR &gt;= v0.7.1, phiên bản SSpanel &gt;=[2021.9](https://github.com/Anankke/SSPanel-Uim/releases/tag/2021.9)，XrayR sẽ kích hoạt các hạn chế thiết bị toàn cầu cho SSpanel. Tại thời điểm này, các nút phụ trợ khác nhau sẽ giới hạn toàn cầu số lượng kết nối IP độc lập, thay vì giới hạn cục bộ của mỗi phần phụ trợ.

Khi giới hạn thiết bị là 1, việc chuyển đổi giữa các nút khác nhau sẽ bị hạn chế. Bạn nên đặt số lượng thiết bị ít nhất là 2. Và do giới hạn bảng điều khiển SSPanel, có thể mất ít nhất 2 phút để thông tin kết nối IP được truyền đến tất cả các nút phụ trợ, vì vậy các kết nối đồng thời trong vòng 2 phút sẽ không bị hạn chế.
