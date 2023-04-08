# Clash Premium Config

### Create Clash Config file

- Directory Structure

  ```tree
  .
  ├── cache.db
  ├── config.yaml
  ├── Country.mmdb
  ├── dashboard
  │   ├── assets
  │   │   ├── index-5e90ca00.js
  │   │   ├── index-6d88662b.css
  │   │   ├── logo-b453e72f.png
  │   │   └── vendor-827b5617.js
  │   ├── CNAME
  │   ├── index.html
  │   ├── manifest.webmanifest
  │   ├── sw.js
  │   └── workbox-e0782b83.js
  ├── proxies
  │   └── subscribe.yaml
  └── ruleset
      ├── apple.yaml
      ├── applications.yaml
      ├── cncidr.yaml
      ├── direct.yaml
      ├── gfw.yaml
      ├── google.yaml
      ├── greatfire.yaml
      ├── icloud.yaml
      ├── lancidr.yaml
      ├── private.yaml
      ├── proxy.yaml
      ├── reject.yaml
      ├── telegramcidr.yaml
      └── tld-not-cn.yaml
  ```

  - Note

    `config.yaml` and `dashboard` are requried。  
    `dashboard` can download from [here](https://github.com/Dreamacro/clash-dashboard/tree/gh-pages)。

- `config.yaml`

  ```yaml
  mixed-port: 7890
  allow-lan: true
  bind-address: '*'
  mode: rule
  log-level: info
  ipv6: true
  external-controller: ':9090'
  external-ui: dashboard
  secret: secret
  tun:
    enable: true
    stack: system
    auto-route: true
    auto-detect-interface: true
  proxy-providers:
    subscribe:
      type: http
      url: 'https://subscribe.com?token=xxxx&flag=clash'
      path: ./proxies/subscribe.yaml
      interval: 86400
      health-check:
        enable: true
        interval: 600
        url: http://www.gstatic.com/generate_204
  proxy-groups:
    - name: '🚀 节点选择'
      type: select
      url: http://www.gstatic.com/generate_204
      interval: 600
      proxies:
        - '🚀 手动切换'
        - '♻️ 自动选择'
        - '🔯 故障转移'
        - '🔮 负载均衡'
      use:
        - subscribe
    - name: '🚀 手动切换'
      type: select
      url: http://www.gstatic.com/generate_204
      interval: 600
      use:
        - subscribe
    - name: '♻️ 自动选择'
      type: url-test
      url: http://www.gstatic.com/generate_204
      interval: 600
      tolerance: 150
      use:
        - subscribe
    - name: '🔯 故障转移'
      type: fallback
      url: http://www.gstatic.com/generate_204
      interval: 600
      use:
        - subscribe
    - name: '🔮 负载均衡'
      type: load-balance
      url: http://www.gstatic.com/generate_204
      interval: 600
      use:
        - subscribe
    - name: '🎥 油管'
      type: select
      url: http://www.gstatic.com/generate_204
      interval: 600
      use:
        - subscribe
    - name: '🎥 奈飞'
      type: select
      url: http://www.gstatic.com/generate_204
      interval: 600
      use:
        - subscribe
    - name: '🎥 迪士尼'
      type: select
      url: http://www.gstatic.com/generate_204
      interval: 600
      use:
        - subscribe
  rule-providers:
    reject:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/reject.txt'
      path: ./ruleset/reject.yaml
      interval: 86400
    icloud:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/icloud.txt'
      path: ./ruleset/icloud.yaml
      interval: 86400
    apple:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/apple.txt'
      path: ./ruleset/apple.yaml
      interval: 86400
    google:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/google.txt'
      path: ./ruleset/google.yaml
      interval: 86400
    proxy:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/proxy.txt'
      path: ./ruleset/proxy.yaml
      interval: 86400
    direct:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/direct.txt'
      path: ./ruleset/direct.yaml
      interval: 86400
    private:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/private.txt'
      path: ./ruleset/private.yaml
      interval: 86400
    gfw:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/gfw.txt'
      path: ./ruleset/gfw.yaml
      interval: 86400
    greatfire:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/greatfire.txt'
      path: ./ruleset/greatfire.yaml
      interval: 86400
    tld-not-cn:
      type: http
      behavior: domain
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/tld-not-cn.txt'
      path: ./ruleset/tld-not-cn.yaml
      interval: 86400
    telegramcidr:
      type: http
      behavior: ipcidr
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/telegramcidr.txt'
      path: ./ruleset/telegramcidr.yaml
      interval: 86400
    cncidr:
      type: http
      behavior: ipcidr
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/cncidr.txt'
      path: ./ruleset/cncidr.yaml
      interval: 86400
    lancidr:
      type: http
      behavior: ipcidr
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/lancidr.txt'
      path: ./ruleset/lancidr.yaml
      interval: 86400
    applications:
      type: http
      behavior: classical
      url: 'https://raw.githubusercontent.com/Loyalsoldier/clash-rules/release/applications.txt'
      path: ./ruleset/applications.yaml
      interval: 86400
  rules:
    - DOMAIN-SUFFIX,subscribe.com,DIRECT
    - RULE-SET,applications,DIRECT
    - RULE-SET,private,DIRECT
    - RULE-SET,reject,REJECT
    - RULE-SET,icloud,DIRECT
    - RULE-SET,apple,DIRECT
    - RULE-SET,google,🚀 节点选择
    - RULE-SET,proxy,🚀 节点选择
    - RULE-SET,direct,DIRECT
    - RULE-SET,lancidr,DIRECT,no-resolve
    - RULE-SET,cncidr,DIRECT,no-resolve
    - RULE-SET,telegramcidr,🚀 节点选择,no-resolve
    - GEOIP,LAN,DIRECT,no-resolve
    - GEOIP,CN,DIRECT,no-resolve
    - MATCH,🚀 节点选择
  ```

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