---
description: HDSD Trojan Qua Nigix
---

# Nginx + Trojan - Sử dụng Nigix Chạy trojan

Sử dụng Nginx để xử lý TLS của Trojan, Trojan rơi trở lại. Tôi xin được gọi anh ấy là một vị thần trong lúc này!

## Cài đặt Nginx

CentOS：

```
 yum update
 yum install -y nginx
 yum install nginx-mod-stream
```

Ubuntu/Debian:

```
 apt update
 apt install nginx
```

## Cấu hình Nginx

Sửa đổi tệp cấu hình /etc/nginx/nginx.conf:

```
stream {
    server {
        listen              443 ssl;                    # Đặt Port thành 443

        ssl_protocols       TLSv1.2 TLSv1.3;      # Đặt phiên bản giao thức SSL được sử dụng

        ssl_certificate /etc/nginx/ssl/xx.com.pem; # địa chỉ chứng chỉ
        ssl_certificate_key /etc/nginx/ssl/xx.com.key; # Địa chỉ khóa bí mật
        ssl_session_cache   shared:SSL:10m;             # Bộ đệm ẩn phiên SSL TCP đã đặt tên cho vùng bộ nhớ được chia sẻ
                                                        # SSL, kích thước vùng là 10MB
        ssl_session_timeout 10m;                        # Thời gian chờ của bộ nhớ cache phiên SSL TCP là 10 phút
        proxy_protocol    on; # Mở proxy_protocol để lấy ip thực
        proxy_pass        127.0.0.1:1234; # Cổng lắng nghe Trojan phụ trợ
    }
}
```

Vui lòng thêm mã trên vào dòng giữa \*\* http \*\* và \*\* sự kiện \*\*

**Tham chiếu tệp cấu hình \*\* / etc / nginx / nginx.conf:**

```
events {
    worker_connections 768;
    # multi_accept on;
}

stream {
    server {
        listen              443 ssl;                    # Đặt Port thành 443

        ssl_protocols       TLSv1.2 TLSv1.3;      # Đặt phiên bản giao thức SSL được sử dụng

        ssl_certificate /etc/nginx/ssl/xx.com.pem; # địa chỉ chứng chỉ
        ssl_certificate_key /etc/nginx/ssl/xx.com.key; # Địa chỉ khóa bí mật
        ssl_session_cache   shared:SSL:10m;             # Bộ đệm ẩn phiên SSL TCP đã đặt tên cho vùng bộ nhớ được chia sẻ
                                                        # SSL, kích thước vùng là 10MB
        ssl_session_timeout 10m;                        # Thời gian chờ của bộ nhớ cache phiên SSL TCP là 10 phút
        proxy_protocol    on; # Mở proxy_protocol để lấy ip thực
        proxy_pass        127.0.0.1:1234; # Cổng lắng nghe Trojan phụ trợ
    }
}

http {

    ##
    # Basic Settings
    ##
```

**Các biện pháp phòng ngừa:**

**1. Vui lòng định cấu hình chứng chỉ SSL**

**2. proxy \ \_pass 127.0.0.1:1234 Cổng lắng nghe Trojan phụ trợ giống như cổng lắng nghe nút giao diện người dùng trên trang web của bạn**

**3. Có thể sửa đổi cổng nghe theo ý muốn từ 1-65535, đây là cổng kết nối máy khách**

## Cấu hình Trojan XrayR

**cấu hình chính：**

```
ListenIP: 127.0.0.1
EnableProxyProtocol: true
EnableFallback: true
CertMode: none
```

{% hint style="info" %}
Lưu ý 1: Đảm bảo rằng không có CertMode và để Nginx xử lý tls
{% endhint %}

{% hint style="info" %}
Lưu ý 2: Hãy đảm bảo rằng trang web dự phòng là http1.1 khi quay lại. Nếu nginx có trang web là h2, nó sẽ khiến tất cả các trang web trở thành h2 (hố khổng lồ)
{% endhint %}

\*\* Toàn bộ ví dụ \*\*

```
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

```
systemctl restart nginx
XrayR restart
```

```
systemctl status nginx
XrayR status
```
