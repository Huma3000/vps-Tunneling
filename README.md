# **VPS服务器搭建，S-UI隧道协议VMess、VLESS、Trojan、Shadowsocks、Hysteria2、TUIC** 

## VPS服务器
1.<-- [vultr](https://www.vultr.com/?ref=9863503) -->

2.<-- [搬瓦工](www.bwh88.net) -->

<-- [推特](https://x.com/OneFangOne) -->


## 以下是 在 VPS 上安装 S-UI 面板（基于 Sing-box 内核） 的详细、保姆级步骤。
S-UI 是目前比较流行的 Sing-box 可视化管理面板，支持 VMess、VLESS、Trojan、Shadowsocks、Hysteria2、TUIC 等多种协议，界面简洁，支持订阅、流量统计、多用户等功能。
推荐系统：Ubuntu 20.04 / 22.04 / Debian 11 / 12（推荐干净系统，amd64 架构）
最低配置：1核1GB 内存即可，建议 2核2GB+ 以防卡顿
#### 注意：本教程仅供学习和个人研究使用，请遵守当地法律法规，严禁用于非法目的。



### 一.准备 VPS 环境（必须 root 执行）一键更新 

```bash
sudo -i
# 更新系统并安装必要工具（Ubuntu/Debian）
apt update && apt upgrade -y
apt install -y curl wget git sudo
```

### 二.一键安装 S-UI（最推荐方式）

```bash
VERSION=1.2.2 && bash <(curl -Ls https://raw.githubusercontent.com/alireza0/s-ui/$VERSION/install.sh) $VERSION
```
一键安装 3x-UI（最推荐方式）
```bash
搭建后如果vless节点无法使用，请尝试更换目标域名(SNI)或者浏览器指纹(fingerprint)
```



### 三.访问面板并登录浏览器打开：
http://你的VPS_IP:你设置的端口/你设置的路径
例如：http://123.45.67.89:25431/Huma3000/
登录后第一时间：去 “设置” → “管理员” 或 “用户管理” 修改密码（如果安装时没改）。
也可以开启 HTTPS（推荐）：用 acme.sh 或 certbot 申请免费证书，然后在面板设置里填入证书路径。



### 四.快速搭建节点示例（面板操作）
#### VMess + WS + TLS（经典.推荐.抗封锁强）
1.面板 → “TLS设置” → “添加reality” → “添加tls”
添加reality：sni和服务器 输入测试延迟保存的域名
生成公钥私钥
添加tls：开启 允许不安全 tls设置开启sni和alpn
sni输入测试延迟保存的域名

2.面板 → “入站管理” → “添加vless” 
监听端口：443（推荐）或随机高端口
模版选择创建的reality
2.面板 → “用户管理” → “添加用户” 
保存 → 重启 sing-box


Reality寻找适合的目标网站
查询ASN：https://tools.ipip.net/as.php

寻找目标：https://fofa.info

asn=="25820" && country=="US" && port=="443" && cert!="Let's Encrypt" && cert.issuer!="ZeroSSL" && status_code="200"

查询IP信息：https://ipinfo.io

ip欺诈值查询：https://scamalytics.com/ip

国家字母代码：https://zh.wikipedia.org/wiki/ISO_3166-1

搜索任意国家：https://www.shodan.io/search/facet?facet=isp&query=http.html%3Aassets%2Fqs%2Fqs.min.js+country%3A

检测端口是否被封 https://tcp.ping.pe/

国家公共DNS：https://public-dns.info/#countries

#### 检测Reality目标域名命令

```bash
======================================
 
  <textarea id="commandBox" readonly="" style=""></textarea>
```
## 推荐代理工具


各平台客户端

Windows（v2rayN）：https://github.com/2dust/v2rayN/releases/tag/6.23

Android（v2rayNG）：https://github.com/2dust/v2rayNG/releases/tag/1.8.5

IOS（shadowrocket）：https://apps.apple.com/app/shadowrocket/id932747118



