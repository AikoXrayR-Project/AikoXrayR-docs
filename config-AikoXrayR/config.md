# Mô tả tệp cấu hình

## Định dạng tệp cấu hình

1. Tệp cấu hình chính có định dạng `yaml` và có tên là` xxx.yml`.
2. Theo mặc định, XrayR sẽ sử dụng `config.yml` trong thư mục chạy phần mềm làm tệp cấu hình.

Định dạng cơ bản của tệp cấu hình, nhiều bảng và nhiều thông tin cấu hình nút có thể được thêm vào cùng một lúc trong Nodes, chỉ cần thêm các mục Nodes ở cùng một định dạng.

```yaml
Log:
  Level: none # Log level: none, error, warning, info, debug 
  AccessPath: # /etc/XrayR/access.Log
  ErrorPath: # /etc/XrayR/error.log
DnsConfigPath: # /etc/XrayR/dns.json Path to dns config, check https://xtls.github.io/config/base/dns/ for help
RouteConfigPath: # /etc/XrayR/route.json # Path to route config, check https://xtls.github.io/config/base/route/ for help
OutboundConfigPath: # /etc/XrayR/custom_outbound.json # Path to custom outbound config, check https://xtls.github.io/config/base/outbound/ for help
ConnetionConfig:
  Handshake: 4 # Handshake time limit, Second
  ConnIdle: 10 # Connection idle time limit, Second
  UplinkOnly: 2 # Time limit when the connection downstream is closed, Second
  DownlinkOnly: 4 # Time limit when the connection is closed after the uplink is closed, Second
  BufferSize: 64 # The internal cache size of each connection, kB 
Nodes:
  -
    PanelType: "SSpanel" # Panel type: SSpanel, V2board, PMpanel, Proxypanel
    ApiConfig:
      ApiHost: "http://127.0.0.1:667"
      ApiKey: "123"
      NodeID: 41
      NodeType: V2ray # Node type: V2ray, Trojan, Shadowsocks, Shadowsocks-Plugin
      Timeout: 30 # Timeout for the api request
      EnableVless: false # Enable Vless for V2ray Type
      EnableXTLS: false # Enable XTLS for V2ray and Trojan
      SpeedLimit: 0 # Mbps, Local settings will replace remote settings, 0 means disable
      DeviceLimit: 0 # Local settings will replace remote settings, 0 means disable
      RuleListPath: # /etc/XrayR/rulelist Path to local rulelist file
    ControllerConfig:
      ListenIP: 0.0.0.0 # IP address you want to listen
      SendIP: 0.0.0.0 # IP address you want to send pacakage
      UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
      EnableDNS: false # Use custom DNS config, Please ensure that you set the dns.json well
      DNSType: AsIs # AsIs, UseIP, UseIPv4, UseIPv6, DNS strategy
      DisableUploadTraffic: false # Disable Upload Traffic to the panel
      DisableGetRule: false # Disable Get Rule from the panel
      DisableIVCheck: false # Disable the anti-reply protection for Shadowsocks
      DisableSniffing: false # Disable domain sniffing 
      EnableProxyProtocol: false # Only works for WebSocket and TCP
      EnableFallback: false # Only support for Trojan and Vless
      FallBackConfigs:  # Support multiple fallbacks
        -
          SNI: # TLS SNI(Server Name Indication), Empty for any
          Path: # HTTP PATH, Empty for any
          Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/fallback/ for details.
          ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for dsable
      CertConfig:
        CertMode: dns # Option about how to get certificate: none, file, http, dns. Choose "none" will forcedly disable the tls config.
        CertDomain: "node1.test.com" # Domain to cert
        CertFile: /etc/XrayR/cert/node1.test.com.cert # Provided if the CertMode is file
        KeyFile: /etc/XrayR/cert/node1.test.com.key
        Provider: alidns # DNS cert provider, Get the full support list here: https://go-acme.github.io/lego/dns/
        Email: test@me.com
        DNSEnv: # DNS ENV option used by DNS provider
          ALICLOUD_ACCESS_KEY: aaa
          ALICLOUD_SECRET_KEY: bbb
  -
    PanelType: "V2board" # Panel type: SSpanel, V2board
    ApiConfig:
      ApiHost: "http://V2board.com"
      ApiKey: "123"
      NodeID: 42
      NodeType: Trojan # Node type: V2ray, Shadowsocks, Trojan
      Timeout: 30 # Timeout for the api request
      EnableVless: false # Enable Vless for V2ray Type, Prefer remote configuration
      EnableXTLS: false # Enable XTLS for V2ray and Trojan， Prefer remote configuration
    ControllerConfig:
      ListenIP: 0.0.0.0 # IP address you want to listen
      UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
      EnableDNS: false # Enable custom DNS config, Please ensure that you set the dns.json well
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

## Mô tả cài đặt tệp cấu hình
### Cấu hình cơ bản

Cấu hình cơ bản là cấu hình có hiệu lực trên tất cả các nút。

```yaml
Log:
  Level: debug # Log level: none, error, warning, info, debug 
  AccessPath: # /etc/XrayR/access.Log
  ErrorPath: # /etc/XrayR/error.log
DnsConfigPath: # /etc/XrayR/dns.json Path to dns config, check https://xtls.github.io/config/base/dns/ for help
RouteConfigPath: # /etc/XrayR/route.json # Path to route config, check https://xtls.github.io/config/base/route/ for help
OutboundConfigPath: # /etc/XrayR/custom_outbound.json # Path to custom outbound config, check https://xtls.github.io/config/base/outbound/ for help
ConnetionConfig:
  Handshake: 4 # Handshake time limit, Second
  ConnIdle: 10 # Connection idle time limit, Second
  UplinkOnly: 2 # Time limit when the connection downstream is closed, Second
  DownlinkOnly: 4 # Time limit when the connection is closed after the uplink is closed, Second
  BufferSize: 64 # The internal cache size of each connection, kB
```

#### cấu hình nhật ký

Cấu hình nhật ký được sử dụng để kiểm soát cấp độ nhật ký của XrayR-core

```yaml
Log:
  Level: debug # Log level: none, error, warning, info, debug 
  AccessPath: # /etc/XrayR/access.Log
  ErrorPath: # /etc/XrayR/error.log
```

| tham số      | Tùy chọn                                      | hướng dẫn                                         |
| ------------ | ----------------------------------------------| ----------------------------------------------    |
| `Level`      | `none`,`error`,`warning`,`info`,`debug`       | Mức hiển thị nhật ký, `không` không được hiển thị |
| `AccessPath` | không                                         | Đường dẫn để lưu nhật ký Access                   |
| `ErrorPath`  | không                                         | Đường dẫn để lưu Nhật ký lỗi                      |

#### Cấu hình DNS tùy chỉnh

Chỉ định đường dẫn đến tệp cấu hình DNS tùy chỉnh

```yaml
DnsConfigPath: # /etc/XrayR/dns.json  Path to dns config
```

| tham số         | Tùy chọn| hướng dẫn                                |
| --------------- | ----    | ---------------------------------------- |
| `DnsConfigPath` | Không   | Đường dẫn đến tệp cấu hình DNS tùy chỉnh |

#### Cấu hình định tuyến tùy chỉnh

Chỉ định đường dẫn tệp cấu hình tuyến đường

```yaml
RouteConfigPath: # /etc/XrayR/route.json # Path to route config, check https://xtls.github.io/config/base/route/ for help
```

| tham số           | Tùy chọn| hướng dẫn                                       | 
| ----------------- | ----    | ------------------------ --------------------   |
| `RouteConfigPath` | Không   | Đường dẫn đến tệp cấu hình định tuyến tùy chỉnh |

#### Cấu hình xuất tùy chỉnh

Chỉ định đường dẫn tệp hồ sơ xuất

```yaml
OutboundConfigPath: # /etc/XrayR/custom_outbound.json # Path to custom outbound config, check https://xtls.github.io/config/base/outbound/ for help
```

| tham số              | Tùy chọn| hướng dẫn                                 |
| -------------------- | ----    | ----------------------------------------  |
| `OutboundConfigPath` | không   | Đường dẫn đến tệp cấu hình xuất tùy chỉnh |

#### kiểm soát kết nối

Tùy chỉnh cấu hình liên quan của bản phát hành kết nối, có thể tối ưu hóa việc sử dụng bộ nhớ ở một mức độ nhất định

```yaml
ConnetionConfig:
  Handshake: 4 # Handshake time limit, Second
  ConnIdle: 10 # Connection idle time limit, Second
  UplinkOnly: 2 # Time limit when the connection downstream is closed, Second
  DownlinkOnly: 4 # Time limit when the connection is closed after the uplink is closed, Second
  BufferSize: 64 # The internal cache size of each connection, kB
```

| tham số          | Tùy chọn| hướng dẫn                                                                                                                                                                                           |
| -------------- | ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Handshake`    | Không    | Giới hạn thời gian bắt tay khi kết nối được thiết lập. Đơn vị là giây. Giá trị mặc định là 4. Khi proxy gửi đến xử lý một kết nối mới, nếu nó mất nhiều thời gian hơn thời gian này trong giai đoạn bắt tay, thì kết nối đó sẽ bị hủy.                                                              |
| `ConnIdle`     | Không    | Giới hạn thời gian để kết nối không hoạt động. Đơn vị là giây. Giá trị mặc định là 10. Nếu không có dữ liệu nào được truyền (cả ngược dòng và xuôi dòng) trong thời gian `ConnIdle`, kết nối sẽ bị ngắt. ** Giảm giá trị này có thể tối ưu hóa việc sử dụng bộ nhớ, nhưng nó sẽ dẫn đến độ trễ kết nối người dùng cao hơn **. |
| `UplinkOnly`   | Không    | Giới hạn thời gian mà đường xuống của kết nối bị đóng. Đơn vị là giây. Giá trị mặc định là 2. Khi máy chủ (chẳng hạn như một trang web từ xa) đóng kết nối đường xuống, proxy gửi đi sẽ ngắt kết nối sau khi đợi thời gian `UplinkOnly`.                           |
| `DownlinkOnly` | Không    | Giới hạn thời gian mà sau đó đường lên được kết nối bị đóng. Đơn vị là giây. Giá trị mặc định là 4. Khi máy chủ (chẳng hạn như một trang web từ xa) đóng kết nối ngược dòng, proxy gửi đi sẽ ngắt kết nối sau khi đợi thời gian `DownlinkOnly`.                        |
| `BufferSize`   | Không    | Kích thước bộ nhớ đệm nội bộ trên mỗi kết nối. Đơn vị là kB. Khi giá trị bằng 0, bộ nhớ đệm bên trong bị vô hiệu hóa. **Giảm giá trị này có thể tối ưu hóa việc sử dụng bộ nhớ, nhưng có thể dẫn đến tăng mức sử dụng CPU**                                      |

Mẹo: 1. Giảm `ConnIdle` có thể tối ưu hóa việc sử dụng bộ nhớ khi số lượng kết nối nhiều, nhưng nó sẽ dẫn đến độ trễ kết nối của người dùng cao hơn. 2. Trong kịch bản duyệt HTTP, có thể đặt `UplinkOnly` và` DownlinkOnly` thành 0 để cải thiện hiệu quả của việc đóng kết nối và giảm mức sử dụng bộ nhớ. 3. Giảm `BufferSize` có thể tối ưu hóa việc sử dụng bộ nhớ, nhưng có thể làm tăng mức sử dụng CPU.

### Cấu hình nút

Mỗi nút là một cấu hình độc lập và sẽ không ảnh hưởng đến nhau. XrayR hỗ trợ khởi động và kết nối đa nút đơn phiên bản với nhiều nút cùng một lúc.

```yaml
Nodes:
  -
    PanelType: "SSpanel" # Panel type: SSpanel, V2board, PMpanel
    ApiConfig:
      ApiHost: "http://127.0.0.1:667"
      ApiKey: "123"
      NodeID: 41
      NodeType: V2ray # Node type: V2ray, Trojan, Shadowsocks, Shadowsocks-Plugin
      Timeout: 30 # Timeout for the api request, Default is 5 sec
      EnableVless: false # Enable Vless for V2ray Type
      EnableXTLS: false # Enable XTLS for V2ray and Trojan
      SpeedLimit: 0 # Mbps, Local settings will replace remote settings, 0 means disable
      DeviceLimit: 0 # Local settings will replace remote settings, 0 means disable
      RuleListPath: # /etc/XrayR/rulelist Path to local rulelist file
    ControllerConfig:
      ListenIP: 0.0.0.0 # IP address you want to listen
      SendIP: 0.0.0.0 # IP address you want to send pacakage
      UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
      EnableDNS: false # Use custom DNS config, Please ensure that you set the dns.json well
      DNSType: AsIs # AsIs, UseIP, UseIPv4, UseIPv6, DNS strategy
      DisableUploadTraffic: false # Disable Upload Traffic to the panel
      DisableGetRule: false # Disable Get Rule from the panel 
      EnableProxyProtocol: false # Only works for WebSocket and TCP
      EnableFallback: false # Only support for Trojan and Vless
      FallBackConfigs:  # Support multiple fallbacks
        -
          SNI: # TLS SNI(Server Name Indication), Empty for any
          Path: # HTTP PATH, Empty for any
          Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/fallback/ for details.
          ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for dsable
      CertConfig:
        CertMode: dns # Option about how to get certificate: none, file, http, dns. Choose "none" will forcedly disable the tls config.
        CertDomain: "node1.test.com" # Domain to cert
        CertFile: /etc/XrayR/cert/node1.test.com.cert # Provided if the CertMode is file
        KeyFile: /etc/XrayR/cert/node1.test.com.key
        Provider: alidns # DNS cert provider, Get the full support list here: https://go-acme.github.io/lego/dns/
        Email: test@me.com
        DNSEnv: # DNS ENV option used by DNS provider
          ALICLOUD_ACCESS_KEY: aaa
          ALICLOUD_SECRET_KEY: bbb
  -
    PanelType: "V2board" # Panel type: SSpanel, V2board, PMpanel
    ApiConfig:
      ApiHost: "http://V2board.com"
      ApiKey: "123"
      NodeID: 42
      NodeType: Trojan # Node type: V2ray, Shadowsocks, Trojan
      Timeout: 30 # Timeout for the api request
      EnableVless: false # Enable Vless for V2ray Type
      EnableXTLS: false # Enable XTLS for V2ray and Trojan
      SpeedLimit: 0 # Local settings will replace remote settings, 0 means disable
      DeviceLimit: 0 # Local settings will replace remote settings, 0 means disable
      RuleListPath: # /etc/XrayR/rulelist Path to local rulelist file
    ControllerConfig:
      ListenIP: 0.0.0.0 # IP address you want to listen
      UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
      EnableDNS: false # Enable custom DNS config, Please ensure that you set the dns.json well
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

#### 面板选择

```yaml
PanelType: "V2board" # Panel type: SSpanel, V2board, PMpanel, Proxypanel
```

| tham số     | Tùy chọn                                    | hướng dẫn                              |
| ----------- | ------------------------------------------ | ----------------                       |
| `PanelType` | `SSPanel`,`V2board`,`PMpanel`,`Proxypanel` | Loại bảng điều khiển phía trước gắn đế |

#### 面板对接配置

```yaml
ApiConfig:
    ApiHost: "http://127.0.0.1:667"
    ApiKey: "123"
    NodeID: 41
    NodeType: V2ray # Node type: V2ray, Trojan, Shadowsocks, Shadowsocks-Plugin
    Timeout: 30 # Timeout for the api request, Default is 5 sec
    EnableVless: false # Enable Vless for V2ray Type
    EnableXTLS: false # Enable XTLS for V2ray and Trojan
    SpeedLimit: 0 # Local settings will replace remote settings, 0 means disable
    DeviceLimit: 0 # Local settings will replace remote settings, 0 means disable
    RuleListPath: # /etc/XrayR/rulelist Path to local rulelist file
    DisableCustomConfig: false # Disable custom config
```

| tham số                 | Tùy chọn                                                | hướng dẫn                                               |
| --------------------- | ---------------------------------------------------- | ------------------------------------------------- |
| `ApiHost`             | Không                                                    | Gắn địa chỉ của bảng điều khiển phía trước                                  |
| `ApiKey`              | Không                                                    | Phím giao tiếp docking front-end                                |
| `NodeID`              | Không                                                    | ID nút                                           |
| `NodeType`            | `V2ray`,`Shadowsocks`, `Shadowsocks-Plugin`,`Trojan` | Loại nút                                          |
| `Timeout`             | Không                                                    | Đặt thời gian chờ cho một lần truy cập vào API, mặc định là 5 giây                  |
| `EnableVless`         | `true`,`false`                                       | Có bật giao thức Vless cho V2ray hay không                         |
| `EnableXTLS`          | `true`,`false`                                       | Có sử dụng XTLS không                                      |
| `SpeedLimit`          | float                                                | Đơn vị là Mbps, cài đặt giới hạn tốc độ cục bộ sẽ ghi đè cài đặt từ xa, 0 có nghĩa là không được bật |
| `DeviceLimit`         | int                                                  |Giới hạn thiết bị cục bộ, sẽ ghi đè cài đặt từ xa, 0 không được bật           |
| `RuleListPath`        | Không                                                    | Cài đặt quy tắc cục bộ, chỉ định đường dẫn tệp quy tắc cục bộ, định dạng tệp quy tắc |
| `DisableCustomConfig` | `true`,`false`                                       | Có bật custom_config hay không, default false              |

#### 后端相关配置

```yaml
ControllerConfig:
  ListenIP: 0.0.0.0 # IP address you want to listen
  SendIP: 0.0.0.0 # IP address you want to send pacakage
  UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
  EnableDNS: false # Use custom DNS config, Please ensure that you set the dns.json well
  DNSType: AsIs # AsIs, UseIP, UseIPv4, UseIPv6, DNS strategy
  DisableUploadTraffic: false # Disable Upload Traffic to the panel
  DisableGetRule: false # Disable Get Rule from the panel
  DisableIVCheck: false # Disable the anti-reply protection for Shadowsocks
  DisableSniffing: false # Disable domain sniffing 
  EnableProxyProtocol: false # Only works for WebSocket and TCP
  EnableFallback: false # Only support for Trojan and Vless
  FallBackConfigs:  # Support multiple fallbacks
    -
      SNI: # TLS SNI(Server Name Indication), Empty for any
      Path: # HTTP PATH, Empty for any
      Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/fallback/ for details.
      ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for dsable
```

| tham số                  | Tùy chọn                              | hướng dẫn                                                                                                                                  |
| ---------------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `ListenIP`             | Không                                  | Chọn địa chỉ IP nghe, `0.0.0.0` sẽ nghe cả v6 và v4                       |
| `SendIP`               | Không                                  | Địa chỉ IP để gửi dữ liệu                                            |
| `UpdatePeriodic`       | Không                                  | Khoảng thời gian để cập nhật nút, thông tin người dùng và báo cáo thông tin sử dụng của người dùng từ giao diện người dùng, mặc định là 60 giây        |
| `EnableDNS`            | `true`,`false`                     | Có bật DNS tùy chỉnh cho nút hiện tại hay không, hãy sử dụng DNS hệ thống theo mặc định                           |
| `DNSType`              | `AsIs`,`UseIP`,`UseIPv4`,`UseIPv6` | Loại phân giải DNS, `AsIs`: sử dụng DNS hệ thống,` UseIP`, `UseIPv4`,` UseIPv6` để sử dụng DNS tùy chỉnh, vui lòng đảm bảo rằng `EnableDNS` là` đúng thực tế '' và `DnsConfigPath` được định cấu hình chính xác|
| `DisableUploadTraffic` | `false`, `true`                    |Có cấm tải lên lưu lượng nút hay không, mặc định là `false`                                          |
| `DisableGetRule`       | `false`, `true`                    |Có cấm nhận các quy tắc từ xa hay không, mặc định là `false`                                          |
| `DisableIVCheck`       | `false`, `true`                    | Có tắt bộ lọc Bloom được Shadowsocks sử dụng để ngăn các cuộc tấn công phát lại hay không, mặc định là `false`               |
| `DisableSniffing`      | `false`, `true`                    | Có tắt tính năng dò tìm miền hay không, mặc định là `false`                                       |
| `EnableProxyProtocol`  | `true`,`false`                     |Có bật ProxyProtocol cho nút hiện tại để lấy IP chuyển tiếp hay không, chỉ hợp lệ cho TCP và WS            |
| `EnableFallback`       | `true`,`false`                     |Có bật Dự phòng cho nút hiện tại hay không, chỉ hợp lệ cho các giao thức Vless và Trojan               |
| `FallBackConfigs`      | list                               | Cấu hình liên quan đến dự phòng, vui lòng kiểm tra [Chức năng dự phòng hướng dẫn ](../gong-neng-shuo-ming/fallback.md)                                                     |

#### Cấu hình liên quan đến ứng dụng chứng chỉ

XrayR hỗ trợ nhiều cấu hình yêu cầu chứng chỉ tự động. Chứng chỉ được áp dụng sẽ được đặt trong thư mục `cert` của thư mục **config file (config.yml) *.

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

| tham số        | Tùy chọn                      | hướng dẫn                                                                                                                                                                                 |
| ------------ | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `CertMode`   | `none`,`file`,`http`,`dns` | Làm thế nào để nhận được chứng chỉ. `tệp`: Cung cấp thủ công và chỉ định đường dẫn. `http`: Đăng ký qua http, yêu cầu cổng 80. `dns`: Để sử dụng chế độ dns, bạn cần phải xây dựng cấu hình của nhà cung cấp dịch vụ dns có liên quan. `none`: Buộc đóng cài đặt tls và để nginx hoặc caddy xử lý.|
| `CertDomain` | Không                          |Đăng ký tên miền chứng chỉ                                                                                                                      |
| `CertFile`   | Không                          |Đường dẫn chứng chỉ được chỉ định theo cách thủ công                                                                                                                 |
| `KeyFile`    | Không                          |Đường dẫn khóa cá nhân được chỉ định theo cách thủ công                                                                                                                |
| `Provider`   | Không                          |Các nhà cung cấp dns, tất cả các nhà cung cấp dns được hỗ trợ có thể được tìm thấy tại đây:[https://go-acme.github.io/lego/dns/](https://go-acme.github.io/lego/dns/)                                                                |
| `DNSEnv`     | Không                          |Đối với các biến môi trường bắt buộc để đăng ký chứng chỉ sử dụng DNS, vui lòng tham khảo liên kết ở trên và điền vào các thông số do nhà cung cấp DNS của riêng bạn yêu cầu. Hãy chú ý đến một dòng trên mỗi dòng và nó phải tuân theo định dạng tệp yaml khi điền vào.    |
