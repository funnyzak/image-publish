# Docker Release 🚀
  
[![Build Status](https://github.com/funnyzak/docker-release/actions/workflows/release.yml/badge.svg)](https://github.com/funnyzak/docker-release)
[![GitHub Container Registry](https://img.shields.io/badge/GHCR-funnyzak-blue)](https://github.com/funnyzak/docker-release)
[![License](https://img.shields.io/github/license/funnyzak/docker-release)](https://github.com/funnyzak/docker-release)

**Docker Release** is a repository that provides Docker images for various services, It publishes images to Docker Hub, GitHub Container Registry, and AliCloud Container Registry. The images are built with the latest source code and are available for multiple architectures.

## Images

All images are provided with the `latest` and `nightly` tags (if available). For other versions, please refer to the Docker Hub or GHCR Container Registry pages.

The following images are available:

- **Nginx**: `funnyzak/nginx:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/nginx))
- **Snell-Server**: `funnyzak/snell-server:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/snell-server))
- **One-API**: `funnyzak/one-api:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/one-api))
- **y-webrtc-signaling Server**: `funnyzak/y-webrtc-signaling:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/y-webrtc-signaling))
- **Abracadabra Demo**: `funnyzak/abracadabra-web:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/abracadabra-web))
- **LibreOffice-Server**: `funnyzak/libreoffice-server:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/libreoffice-server))
- **Request-Hub**: `funnyzak/request-hub:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/request-hub))
- **Canal-Adaptor**: `funnyzak/canal-adapter:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/canal-adapter))
- **Canal-Deployer**: `funnyzak/canal-deployer:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/canal-deployer))
- **Canal-Admin**: `funnyzak/canal-admin:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/canal-admin))
- **Hello-World**: `funnyzak/hello-world:latest` ([Docker Hub](https://hub.docker.com/r/funnyzak/hello-world))


You can pull the above images from Docker Hub, GitHub Container Registry, or Aliyun Container Registry. For example:

- Docker Hub: `docker pull funnyzak/nginx:latest`
- GitHub Container Registry: `docker pull ghcr.io/funnyzak/nginx:latest`
- Aliyun Container Registry: `docker pull registry.cn-beijing.aliyuncs.com/funnyzak/nginx:latest`

## Services

### Nginx

[![Docker Tags](https://img.shields.io/docker/v/funnyzak/nginx?sort=semver&style=flat-square)](https://hub.docker.com/r/funnyzak/nginx/)
[![Image Size](https://img.shields.io/docker/image-size/funnyzak/nginx)](https://hub.docker.com/r/funnyzak/nginx/)
[![Docker Stars](https://img.shields.io/docker/stars/funnyzak/nginx.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/nginx/)
[![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/nginx.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/nginx/)

A nginx docker image with secure configurations and some useful modules, such as `ngx_http_geoip_module`, `ngx_http_image_filter_module`, `ngx_http_perl_module`, `ngx_http_xslt_filter_module`, `ngx_mail_module`, `ngx_stream_geoip_module`, `ngx_stream_module`, `ngx-fancyindex`, `headers-more-nginx-module`, etc.

Build with the  `linux/arm64`, `linux/386`, `linux/amd64`, `linux/arm/v6`, `linux/arm/v7`, `linux/arm64/v8` architectures.


<details>
<summary>Deployment</summary>

**Docker Deployment**:

```bash
docker run -d -t -i --name nginx --restart on-failure \
  -v /path/to/conf.d:/etc/nginx/conf.d \
  -p 1688:80 \
  funnyzak/nginx
```

**Docker Compose Deployment**:
```yaml

version: "3.3"

services:
  nginx:
    image: funnyzak/nginx
    container_name: nginx
    environment:
      - TZ=Asia/Shanghai
    volumes:
      - ./nginx/conf.d:/etc/nginx/conf.d
    restart: on-failure
    ports:
      - 1688:80
```

</details>

For more information, please check [Nginx](https://github.com/funnyzak/docker-release/tree/main/Docker/nginx/README.md).

---

### Snell-Server

[![Docker Tags](https://img.shields.io/docker/v/funnyzak/snell-server?sort=semver&style=flat-square)](https://hub.docker.com/r/funnyzak/snell-server/)
[![Image Size](https://img.shields.io/docker/image-size/funnyzak/snell-server)](https://hub.docker.com/r/funnyzak/snell-server/)
[![Docker Stars](https://img.shields.io/docker/stars/funnyzak/snell-server.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/snell-server/)
[![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/snell-server.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/snell-server/)

Snell Server is a lean encrypted proxy protocol. It is designed to be simple, lightweight.

This image is build from the latest source code of [Snell Server](https://manual.nssurge.com/others/snell.html). It supports `linux/amd64`, `linux/arm64`, `linux/arm/v7`, `linux/386` architecture. 

> **Notice**: Need to use with Surge iOS or Surge Mac, both of them support Snell protocol. The latest surge-server version is v4, which is not compatible with the previous versions like before. Please upgrade both the client (Surge iOS & Surge Mac) and the server binary.


<details>
<summary>Deployment</summary>

**Docker Deployment**:

```bash
docker run -d --name snell-server --restart always -p 12303:6180 -e PSK="5G0H4qdf32mEZx32t" funnyzak/snell-server
```

**Docker Compose Deployment**:

```yaml
version: '3'

services:
  snell:
    image: funnyzak/snell-server
    container_name: snell-server
    environment:
      PSK: 5G0H4qdf32mEZx32t
      TZ: Asia/Shanghai
      IPV6: false
      PORT: 6180
    restart: always
    ports:
      - 12303:6180
```

**Echo config file**:

```bash
docker exec -it snell-server cat /etc/snell-server.conf
```

</details>

For more information, please check [Snell-Server](https://github.com/funnyzak/docker-release/tree/main/Docker/snell-server/README.md).

---

### One-API

[![Docker Tags](https://img.shields.io/docker/v/funnyzak/one-api?sort=semver&style=flat-square)](https://hub.docker.com/r/funnyzak/one-api/)
[![Image Size](https://img.shields.io/docker/image-size/funnyzak/one-api)](https://hub.docker.com/r/funnyzak/one-api/)
[![Docker Stars](https://img.shields.io/docker/stars/funnyzak/one-api.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/one-api/)
[![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/one-api.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/one-api/)

**One-API** Access all LLM through the standard OpenAI API format, easy to deploy & use. It built with the `linux/amd64`, `linux/arm64` architectures.

<details>
<summary>Deployment</summary>

**Docker Deployment**:

### Docker Deployment
Deployment command: `docker run --name one-api -d --restart always -p 3000:3000 -e TZ=Asia/Shanghai -v /home/ubuntu/data/one-api:/data funnyzak/one-api`

Update command: `docker run --rm -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower -cR`

The first `3000` in `-p 3000:3000` is the port of the host, which can be modified as needed.

Data will be saved in the `/home/ubuntu/data/one-api` directory on the host. Ensure that the directory exists and has write permissions, or change it to a suitable directory.

Nginx reference configuration:
```
server{
   server_name openai.justsong.cn;  # Modify your domain name accordingly

   location / {
          client_max_body_size  64m;
          proxy_http_version 1.1;
          proxy_pass http://localhost:3000;  # Modify your port accordingly
          proxy_set_header Host $host;
          proxy_set_header X-Forwarded-For $remote_addr;
          proxy_cache_bypass $http_upgrade;
          proxy_set_header Accept-Encoding gzip;
   }
}
```

Next, configure HTTPS with Let's Encrypt certbot:
```bash
# Install certbot on Ubuntu:
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
# Generate certificates & modify Nginx configuration
sudo certbot --nginx
# Follow the prompts
# Restart Nginx
sudo service nginx restart
```

The initial account username is `root` and password is `123456`.

</details>

### Y-WebRTC Signaling

[![Docker Tags](https://img.shields.io/docker/v/funnyzak/y-webrtc-signaling?sort=semver&style=flat-square)](https://hub.docker.com/r/funnyzak/y-webrtc-signaling/)
[![Image Size](https://img.shields.io/docker/image-size/funnyzak/y-webrtc-signaling)](https://hub.docker.com/r/funnyzak/y-webrtc-signaling/)
[![Docker Stars](https://img.shields.io/docker/stars/funnyzak/y-webrtc-signaling.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/y-webrtc-signaling/)
[![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/y-webrtc-signaling.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/y-webrtc-signaling/)


Y-WebRTC is a WebRTC signaling server. More information can be found at [y-webrtc-signaling](https://github.com/lobehub/y-webrtc-signaling).

This image is built with the `linux/amd64`, `linux/arm64`, `linux/arm/v7`, `linux/arm64/v8`, `linux/ppc64le`, `linux/s390x` architectures.


<details>
<summary>Deployment</summary>

**Docker Deployment**:

```bash
docker run -d --name y-webrtc-signaling -p 4444:4444 funnyzak/y-webrtc-signaling:latest
```

**Docker Compose Deployment**:

```yaml
version: '3.1'
services:
  y-webrtc-signaling:
    container_name: y-webrtc-signaling
    image: funnyzak/y-webrtc-signaling:latest
    restart: always
    network_mode: bridge
    ports:
      - "4444:4444"
```
</details>

For more information, please check [y-webrtc-signaling](https://github.com/funnyzak/docker-release/tree/main/Docker/y-webrtc-signaling/README.md).

---

### Abracadabra Demo

[![Docker Tags](https://img.shields.io/docker/v/funnyzak/abracadabra-web?sort=semver&style=flat-square)](https://hub.docker.com/r/funnyzak/abracadabra-web/)
[![Image Size](https://img.shields.io/docker/image-size/funnyzak/abracadabra-web)](https://hub.docker.com/r/funnyzak/abracadabra-web/)
[![Docker Stars](https://img.shields.io/docker/stars/funnyzak/abracadabra-web.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/abracadabra-web/)
[![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/abracadabra-web.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/abracadabra-web/)

Abracadabra (魔曰) is an instant text encryption/de-sensitization tool, which can also be used for file encryption, based on C++ 11. More information can be found at [Abracadabra_demo](https://github.com/SheepChef/Abracadabra_demo).

This image is built with the `linux/amd64`, `linux/arm64`, `linux/arm/v7`, `linux/arm64/v8`, `inux/ppc64le`, `linux/s390x` architectures.


<details>
<summary>Deployment</summary>

**Docker Deployment**:

```bash

docker run -d --name abracadabra-web -p 8080:80 funnyzak/abracadabra-web:latest
# ghcr
docker run -d --name abracadabra-web -p 8080:80 ghcr.io/funnyzak/abracadabra-web:latest
# aliyun
docker run -d --name abracadabra-web -p 8080:80 registry.cn-beijing.aliyuncs.com/funnyzak/abracadabra-web:latest
```

**Docker Compose Deployment**:

```yaml
version: '3.1'

services:
  abracadabra-web:
    container_name: abracadabra-web
    image: funnyzak/abracadabra-web:latest
    restart: always
    network_mode: bridge
    ports:
    - "8080:80"
```

**After Startup**:

![Abracadabra_demo](https://cdn.jsdelivr.net/gh/funnyzak/docker-release@main/Docker/abracadabra-web/abracadabra-demo.png)

</details>

For more information, please check [Abracadabra_demo](https://github.com/funnyzak/docker-release/tree/main/Docker/abracadabra-web/README.md).

---

### LibreOffice-Server

[![Docker Tags](https://img.shields.io/docker/v/funnyzak/libreoffice-server?sort=semver&style=flat-square)](https://hub.docker.com/r/funnyzak/libreoffice-server/)
[![Image Size](https://img.shields.io/docker/image-size/funnyzak/libreoffice-server)](https://hub.docker.com/r/funnyzak/libreoffice-server/)
[![Docker Stars](https://img.shields.io/docker/stars/funnyzak/libreoffice-server.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/libreoffice-server/)
[![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/libreoffice-server.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/libreoffice-server/)

LibreOffice Service service for editing documents online and converting Word to PDF via Web API. This service contains a Web API based on [LibreOffice service App](https://github.com/funnyzak/libreoffice-server).

This image is built with the `linux/amd64`, `linux/arm64` architectures.


<details>
<summary>Deployment</summary>

**Docker Deployment**:

```bash
docker run -d --name libreoffice -p 3000:3000 -p 3001:8038 funnyzak/libreoffice-server:latest
```

**Docker Compose Deployment**:

```yaml
version: "3.1"
services:
  libreoffice:
    image: funnyzak/libreoffice-server
    container_name: libreoffice
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Shanghai
    # volumes:
    #   -./media/fonts:/usr/share/fonts/custom # 自定义字体
    ports:
      - 3000:3000 # libreoffice web editor
      - 3001:8038 # web api
    restart: unless-stopped
```
</details>

For more information, please check [LibreOffice-Server](https://github.com/funnyzak/docker-release/tree/main/Docker/libreoffice-server/README.md).

---

### Request-Hub

[![Docker Tags](https://img.shields.io/docker/v/funnyzak/request-hub?sort=semver&style=flat-square)](https://hub.docker.com/r/funnyzak/request-hub/)
[![Image Size](https://img.shields.io/docker/image-size/funnyzak/request-hub)](https://hub.docker.com/r/funnyzak/request-hub/)
[![Docker Stars](https://img.shields.io/docker/stars/funnyzak/request-hub.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/request-hub/)
[![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/request-hub.svg?style=flat-square)](https://hub.docker.com/r/funnyzak/request-hub/)

[RequestHub](https://github.com/kyledayton/requesthub) is used to receive, record, and proxy HTTP requests. This image supports `linux/386`, `linux/amd64`, `linux/arm/v6`, `linux/arm/v7`, `linux/arm64/v8`, `linux/s390x`.


<details>
<summary>Deployment</summary>

**Docker Deployment**:

```bash
docker run -d --name request-hub -p 8080:8080 funnyzak/request-hub:latest
```

**Docker Compose Deployment**:

```yaml
version: '3.1'
services:
  requesthub:
    image: funnyzak/request-hub
    container_name: requesthub
    restart: always
    environment:
        - TZ=Asia/Shanghai
        - LANG=C.UTF-8
        - CONFIG_YML=/config.yml
        - NO_WEB=false
        - PORT=54321
        - MAX_REQUESTS=1024
        - USER_NAME=hello
        - PASSWORD=world
    volumes:
      -./config.yml:/config.yml
    ports:
      - 80:54321
```

**After Deployment**:

![Request-Hub](https://cdn.jsdelivr.net/gh/funnyzak/docker-release@main/Docker/request-hub/request-hub-demo.jpg)

</details>

For more information, please check [Request-Hub](https://github.com/funnyzak/docker-release/tree/main/Docker/request-hub/README.md).

---

### Alibaba Canal

Alibaba Canal, a component for incremental subscription and consumption of binlogs in MySQL.  Images are built for `linux/amd64` and `linux/arm64` architectures.

The following images are available:

| Image | Tag | Size | Pulls |
|---|---|---|---|
| Canal-Adapter | [![Docker Tag](https://img.shields.io/docker/v/funnyzak/canal-adapter/latest?label=Canal-Adapter)](https://hub.docker.com/r/funnyzak/canal-adapter/tags) | [![Docker Image Size](https://img.shields.io/docker/image-size/funnyzak/canal-adapter/latest?label=Canal-Adapter)](https://hub.docker.com/r/funnyzak/canal-adapter/tags) | [![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/canal-adapter?label=Canal-Adapter)](https://hub.docker.com/r/funnyzak/canal-adapter) |
| Canal-Deployer | [![Docker Tag](https://img.shields.io/docker/v/funnyzak/canal-deployer/latest?label=Canal-Deployer)](https://hub.docker.com/r/funnyzak/canal-deployer/tags) | [![Docker Image Size](https://img.shields.io/docker/image-size/funnyzak/canal-deployer/latest?label=Canal-Deployer)](https://hub.docker.com/r/funnyzak/canal-deployer/tags) | [![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/canal-deployer?label=Canal-Deployer)](https://hub.docker.com/r/funnyzak/canal-deployer) |
| Canal-Admin | [![Docker Tag](https://img.shields.io/docker/v/funnyzak/canal-admin/latest?label=Canal-Admin)](https://hub.docker.com/r/funnyzak/canal-admin/tags) | [![Docker Image Size](https://img.shields.io/docker/image-size/funnyzak/canal-admin/latest?label=Canal-Admin)](https://hub.docker.com/r/funnyzak/canal-admin/tags) | [![Docker Pulls](https://img.shields.io/docker/pulls/funnyzak/canal-admin?label=Canal-Admin)](https://hub.docker.com/r/funnyzak/canal-admin) |


All Images are installed under the `/opt/canal` directory.  For example, the `canal-adapter` service is installed under `/opt/canal/canal-adapter`.

<details>
<summary>Docker Pull</summary>

```bash
# Docker Hub
docker pull funnyzak/canal-adapter:latest
docker pull funnyzak/canal-deployer:latest
docker pull funnyzak/canal-admin:latest

# GitHub Container Registry (GHCR)
docker pull ghcr.io/funnyzak/canal-adapter:latest
docker pull ghcr.io/funnyzak/canal-deployer:latest
docker pull ghcr.io/funnyzak/canal-admin:latest

# Alibaba Cloud Container Registry
docker pull registry.cn-beijing.aliyuncs.com/funnyzak/canal-adapter:latest
docker pull registry.cn-beijing.aliyuncs.com/funnyzak/canal-deployer:latest # Corrected typo here
docker pull registry.cn-beijing.aliyuncs.com/funnyzak/canal-admin:latest
```

</details>


For more information about Canal, please check [Alibaba Canal](https://github.com/funnyzak/docker-release/tree/main/Docker/canal/README.md).

## Directories

Images build directory is located at ./Docker. You can also download the directory to build the images yourself.

- `./Docker/nginx`: Build the [Nginx](https://nginx.org) service image.
- `./Docker/one-api`: Build the [One-API](https://github.com/songquanpeng/one-api) service image.
- `./Docker/snell-server`: Build the [Snell-Server](https://manual.nssurge.com/others/snell.htm) service image.
- `./Docker/y-webrtc-signaling`: Build the [y-webrtc-signaling](https://github.com/lobehub/y-webrtc-signaling) service image.
- `./Docker/abracadabra-web`: Build the [Abracadabra_demo](https://github.com/SheepChef/Abracadabra_demo) service image.
- `./Docker/libreoffice-server`: Build the [LibreOffice-Server](https://github.com/funnyzak/libreoffice-server) service image.
- `./Docker/request-hub`: Build the [Request-Hub](https://github.com/kyledayton/requesthub) service image.
- `./Docker/canal`: Build the [Alibaba Canal](https://github.com/alibaba/canal) service images.


## Contributions

If you have any questions or suggestions, please feel free to open an issue or pull request.

## License

[MIT](https://github.com/funnyzak/docker-release/blob/main/LICENSE)
