# Clash Premium Config

### Create Clash Config file

- Directory Structure

  ```tree
  .
  ├── Country.mmdb
  ├── config.yaml
  ├── custom_rules
  │   ├── direct.yaml
  │   ├── proxy.yaml
  │   └── reject.yaml
  ├── dashboard
  │   ├── CNAME
  │   ├── assets
  │   │   ├── index-5e90ca00.js
  │   │   ├── index-6d88662b.css
  │   │   ├── logo-b453e72f.png
  │   │   └── vendor-827b5617.js
  │   ├── index.html
  │   ├── manifest.webmanifest
  │   ├── sw.js
  │   └── workbox-e0782b83.js
  ├── online_rules
  │   ├── apple.yaml
  │   ├── applications.yaml
  │   ├── cncidr.yaml
  │   ├── direct.yaml
  │   ├── gfw.yaml
  │   ├── google.yaml
  │   ├── greatfire.yaml
  │   ├── icloud.yaml
  │   ├── lancidr.yaml
  │   ├── private.yaml
  │   ├── proxy.yaml
  │   ├── reject.yaml
  │   ├── telegramcidr.yaml
  │   └── tld-not-cn.yaml
  └── proxies
  ```

  - Note

    `config.yaml` and `dashboard` are requried。  
    `dashboard` can download from [here](https://github.com/Dreamacro/clash-dashboard/tree/gh-pages)。
    Add your subscribe address to `./custom_rules/direct.yaml` file.

- [config.yaml](https://github.com/picopock/clash_premium_config/blob/master/config/config.yaml)
  
### Create `tun` device on host

  ```sh
  ip tuntap add dev tun mod tun
  ```

- Delete `tun` device

  ```sh
  ip tuntap del dev tun mod tun
  ```

### Create `clash` container

  ```sh
  docker run -d --net=macvlan --ip=10.0.0.8 --ip6=fc00:1::8 --mac-address=02:42:0a:00:00:08 --name=clash-premium --restart=always --hostname=clash --env TZ=Asia/Shanghai --cap-add=NET_ADMIN --device=/dev/net/tun:/dev/net/tun -v /volume1/docker/clash:/root/.config/clash dreamacro/clash-premium:latest
  ```