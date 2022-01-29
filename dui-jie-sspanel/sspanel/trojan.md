# Kết nối Trojan

| thỏa thuận | Hỗ trợ | | thỏa thuận hỗ trợ
| :--- | :--- | :--- |
| Trojan | √ | tcp, grpc |

## SSpanel-uim nút địa chỉ định dạng

```text
Tên miền hoặc IP; port=cổng kết nối người dùng #cổng nghe|host=xx
```

## tcp ví dụ

```text
Ví dụ: gz.aaa.com; port=443|host=gz.aaa.com
```

## grpc ví dụ

Sử dụng trojan+grpc vui lòng nâng cấp sspanel đến [Anankke/SSPanel-Uim@8f68b63] (https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107)

```text
Ví dụ: gz.aaa.com; port=443|host=gz.aaa.com|grpc=1|servicename=gz.aaa.com
```

## Ví dụ chuyển tiếp

Người dùng kết nối 443, XrayR nghe 12345

```text
Ví dụ: gz.aaa.com; port=443#12345|host=hk.aaa.com
```

## Cho phép xtls **(đây là tính năng thử nghiệm)**

sspanel nâng cấp lên phiên bản này [Anankke/SSPanel-Uim@8f68b63] (https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107) hỗ trợ đăng ký xtls

Thêm 'enable_xtls = true' vào bất kỳ cấu hình giao thức nào và nếu xtls có flow điều khiển luồng, nó sẽ được thêm vào cuối: 'flow =flow-vlaue'

```text
Ví dụ: gz.aaa.com; port=443|host=gz.aaa.com|enable_xtls=true|flow=xtls-rprx-direct
```

Các tập tin được thiết lập tại địa phương đặt 'EnableXTLS' thành true. Hồ sơ được nêu chi tiết: [Mô tả hồ sơ] (https://github.com/XrayR-project/XrayR-doc/tree/af55d4cc45735ca8d00491aa97f8cbbd97c8faf4/sspanel/config/README.md)

