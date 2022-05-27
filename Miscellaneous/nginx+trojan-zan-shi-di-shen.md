# Nginx + Trojan tạm thời nhỏ giọt!

Sử dụng Nginx để xử lý TLS của Trojan, Trojan rơi trở lại. Tôi xin được gọi anh ấy là một vị thần trong lúc này!

## Cài đặt Nginx

CentOS：

```text
 yum update
 yum install -y nginx
 yum install nginx-mod-stream
```

Ubuntu/Debian:

```text
 apt update
 apt install nginx
```

## Cấu hình Nginx

Sửa đổi tệp cấu hình /etc/nginx/nginx.conf:

```text
stream {
    server {
        listen              443 ssl;                    # 设置监听端口为443

        ssl_protocols       TLSv1.2 TLSv1.3;      # 设置使用的SSL协议版本

        ssl_certificate /etc/nginx/ssl/xx.com.pem; # 证书地址
        ssl_certificate_key /etc/nginx/ssl/xx.com.key; # 秘钥地址
        ssl_session_cache   shared:SSL:10m;             # SSL TCP会话缓存设置共享内存区域名为
                                                        # SSL，区域大小为10MB
        ssl_session_timeout 10m;                        # SSL TCP会话缓存超时时间为10分钟
        proxy_protocol    on; # 开启proxy_protocol获取真实ip
        proxy_pass        127.0.0.1:1234; # 后端Trojan监听端口
    }
}
```

Vui lòng thêm mã trên vào dòng giữa ** http ** và ** sự kiện **

**Tham chiếu tệp cấu hình ** / etc / nginx / nginx.conf:**

```text
events {
    worker_connections 768;
    # multi_accept on;
}

stream {
    server {
        listen              443 ssl;                    # 设置监听端口为443

        ssl_protocols       TLSv1.2 TLSv1.3;      # 设置使用的SSL协议版本

        ssl_certificate /etc/nginx/ssl/xx.com.pem; # 证书地址
        ssl_certificate_key /etc/nginx/ssl/xx.com.key; # 秘钥地址
        ssl_session_cache   shared:SSL:10m;             # SSL TCP会话缓存设置共享内存区域名为
                                                        # SSL，区域大小为10MB
        ssl_session_timeout 10m;                        # SSL TCP会话缓存超时时间为10分钟
        proxy_protocol    on; # 开启proxy_protocol获取真实ip
        proxy_pass        127.0.0.1:1234; # 后端Trojan监听端口
    }
}

http {

    ##
    # Basic Settings
    ##
```

**Các biện pháp phòng ngừa:**

**1. Vui lòng định cấu hình chứng chỉ SSL**

**2. proxy \ _pass 127.0.0.1:1234 Cổng lắng nghe Trojan phụ trợ giống như cổng lắng nghe nút giao diện người dùng trên trang web của bạn**

**3. Có thể sửa đổi cổng nghe theo ý muốn từ 1-65535, đây là cổng kết nối máy khách**

## Cấu hình Trojan XrayR

**cấu hình chính：**

```text
ListenIP: 127.0.0.1
EnableProxyProtocol: true
EnableFallback: true
CertMode: none
```

{% hint style="info" %}
注意1：请务必确保CertMode为none，交由Nginx处理tls
{% endhint %}

{% hint style="info" %}
注意2：在回落时请确保回落站点是http1.1，nginx如果有一个站点是h2会导致全部站点都变成h2（巨坑）
{% endhint %}

** Toàn bộ ví dụ **

```text
  -
    PanelType: "SSpanel" # Panel type: SSpanel, V2board, PMpanel
    ApiConfig:
      ApiHost: "https://xxx.com"
      ApiKey: "123"
      NodeID: 1
      NodeType: Trojan # Node type: V2ray, Shadowsocks, Trojan
      Timeout: 10 # Timeout for the api request
      EnableVless: false # Enable Vless for V2ray Type
      EnableXTLS: false # Enable XTLS for V2ray and Trojan
      SpeedLimit: 0 # Mbps, Local settings will replace remote settings, 0 means disable
      DeviceLimit: 0 # Local settings will replace remote settings, 0 means disable
      RuleListPath: # /etc/XrayR/rulelist Path to local rulelist file
    ControllerConfig:
      ListenIP: 127.0.0.1 # IP address you want to listen
      SendIP: 0.0.0.0 # IP address you want to send pacakage
      UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
      EnableDNS: false # Use custom DNS config, Please ensure that you set the dns.json well
      DNSType: AsIs # AsIs, UseIP, UseIPv4, UseIPv6, DNS strategy
      EnableProxyProtocol: true # Only works for WebSocket and TCP
      EnableFallback: true # Only support for Trojan and Vless
      FallBackConfigs:  # Support multiple fallbacks
        -
          SNI: # TLS SNI(Server Name Indication), Empty for any
          Path: # HTTP PATH, Empty for any
          Dest: fake.website.com:80 # Required, Destination of fallback, check https://xtls.github.io/config/fallback/ for details.
          ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for dsable
      CertConfig:
        CertMode: none # Option about how to get certificate: none, file, http, dns. Choose "none" will forcedly disable the tls config.
        CertDomain: "node1.test.com" # Domain to cert
        CertFile: /etc/XrayR/cert/node1.test.com.cert # Provided if the CertMode is file
        KeyFile: /etc/XrayR/cert/node1.test.com.key
        Provider: alidns # DNS cert provider, Get the full support list here: https://go-acme.github.io/lego/dns/
        Email: test@me.com
        DNSEnv: # DNS ENV option used by DNS provider
          ALICLOUD_ACCESS_KEY: aaa
          ALICLOUD_SECRET_KEY: bbb
```

## Khởi động lại và kiểm tra Nginx và XrayR

```text
systemctl restart nginx
XrayR restart
```

```text
systemctl status nginx
XrayR status
```

