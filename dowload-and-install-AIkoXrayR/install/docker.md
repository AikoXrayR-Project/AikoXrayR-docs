# Cài đặt bằng docker

## Cài đặt Docker

### Centos

```bash
yum install -y yum-utils
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce docker-ce-cli containerd.io -y
systemctl start docker
systemctl enable docker
```

### Debian / Ubuntu

```bash
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
systemctl start docker
systemctl enable docker
```

## Cài đặt Docker-compose

```bash
curl -fsSL https://get.docker.com | bash -s docker
curl -L "https://github.com/docker/compose/releases/download/1.26.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

## Docker-compose Cài đặt XrayR \(giới thiệu\)

1. `git clone https://github.com/AikoXrayR-project/AikoXrayR-Dockerinstall`
2. `cd AikoXrayR-Dockerinstall`
3. Chỉnh sửa tệp cấu hình：`config.yml`，xem chi tiết：[Mô tả tệp cấu hình](../../config-AikoXrayR/config.md)
4. Chạy docker：`docker-compose up -d`

## Docker run Cài đặt XrayR

Hãy cẩn thận chỉ định thư mục `config.yml`.

```bash
docker pull aikocute/xrayr:latest && docker run --restart=always --name xrayr -d -v ${PATH_TO_CONFIG}/config.yml:/etc/XrayR/config.yml --network=host aikocute/xrayr:latest
```

## Cập nhật XrayR

docker-composeCập nhật, xóa vùng chứa và khởi động lại chỉ với hai lệnh đơn giản và chung chung. `config.yml` sẽ không bị bản cập nhật ghi đè sau khi cập nhật phần mềm.

Lưu ý rằng thực thi trong thư mục chứa docker-compose.yml:

```bash
docker-compose pull
docker-compose up -d
```

