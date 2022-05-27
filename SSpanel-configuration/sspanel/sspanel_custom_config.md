# Kết nối với phiên bản mới SSPanel Custom Config

Đối với phương pháp cấu hình tự động kích hoạt Custom_config trong phiên bản sspanel > = 2021.11, hãy xem cấu hình sau để cấu hình thông tin nút chính xác. Để biết thông tin về đăng ký, hãy xem tài liệu liên quan đến SSPanel: https://wiki.sspanel.org/#/universal-subscription.
Nếu bạn không muốn sử dụngcustom config, hãy đặt 'DisableCustomConfig' thành 'true', trong 'ApiConfig'.

# Shadowsocks
```json
{
	"offset_port_user": "12345", cổng được phát hành trong //front-end/đăng ký
    "offset_port_node": "12345", //cổng được phát hành bởi máy chủ nút
    "server_user": "hk.domain.com", //front-end/đăng ký trong địa chỉ máy chủ được phát hành
    "mu_encryption": "chacha20-ietf-poly1305", // 'aes-128-gcm', 'aes-256-gcm', 'chacha20-ietf-poly1305'
}

```

# V2ray

AlterId được đặt thành 0 và VMessAEAD sẽ được kích hoạt tự động.

{% hint style="info" %} Lưu ý: VMESS AEAD sẽ bắt buộc bật vào ngày 1 tháng 1 năm 2022 Xin lưu ý cập nhật cấu hình phía dịch vụ, thiết lập alterId = 0 {% endhint %}

## tcp Ví dụ

``` json
{
	"offset_port_node": 12345,
	"server_sub": "hk.domain.com",
	"alter_id": 0,
	"network": "tcp",
	"security": "none",
}
```

## tcp+http Ví dụ

```json
{
	"offset_port_node": 12345,
	"server_sub": "hk.domain.com",
	"alter_id": 0,
	"network": "tcp",
	"security": "none",
	"header": {
        "type": "http",
        "request": {
            "path": ["/"],
  			"headers": {
    			"Host": ["www.baidu.com"]
            }
        },
        "response": {}
    }
}
```

## tcp+tls Ví dụ

```json
{
	"offset_port_node": 443,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": 0,
	"network": "tcp",
	"security": "tls",
}
```

## ws Ví dụ

```json
{
	"offset_port_node": 80,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": 0,
	"network": "ws",
	"security": "none",
	"path": "/v2ray"
}
```

## ws+tls Ví dụ

```json
{
	"offset_port_node": 443,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": 0,
	"network": "ws",
	"security": "tls",
	"path": "/v2ray"
}
```

## grpc+tls Ví dụ

```json
{
	"offset_port_node": 443,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": 0,
	"network": "grpc",
	"security": "tls",
	"servicename": "some_name"
}
```

## Ví dụ về cổng xoay
Đặt 'offset_port_user' cho người dùng trong bất kỳ cấu hình nào

``` json
{
	"offset_port_user": 8888,
	"offset_port_node": 12345,
	"server_sub": "hk.domain.com",
	"alter_id": 0,
	"network": "tcp",
	"security": "none",
}
```

Tại thời điểm này, cổng kết nối người dùng là 8888 và cổng nghe nút là 12345

## Bật vless
Đặt 'enable_vless: 1' cho người dùng để kết nối cổng trong bất kỳ cấu hình nào

``` json
{
	"offset_port_node": 443,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": 0,
	"network": "tcp",
	"security": "tls",
	"enable_vless": 1
}
```
Vui lòng bật vless và luôn luôn sử dụng tls hoặc xtls.

## Cho phép xtls
Thiết lập 'security: xtls'trong bất kỳ cấu hình nào.

``` json
{
	"offset_port_node": 443,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": 0,
	"network": "tcp",
	"security": "xtls",
	"enable_vless": 1
}
```

# Trojan

## tcp Ví dụ

``` json
{
	"offset_port_node": 443,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com"
}
```

## grpc Ví dụ

``` json
{
	"offset_port_node": 443,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"grpc": 1,
	"servicename": "some_name"
}
```

## Ví dụ chuyển tiếp
Đặt 'offset_port_user' cho người dùng trong bất kỳ cấu hình nào
``` json
{
	"offset_port_user": 443,
	"offset_port_node": 12345,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com"
}
```
Tại thời điểm này người dùng kết nối 443, nút lắng nghe 12345

## Cho phép xtls

Đặt 'enable_xtls: 1' trong bất kỳ cấu hình nào.

``` json
{
	"offset_port_node": 443,
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"enable_xtls": 1
}
```