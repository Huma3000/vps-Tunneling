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
# 更新系统并安装必要工具（Ubuntu/Debian）
apt update && apt upgrade -y
apt install -y curl wget git sudo
```

### 二.一键安装 S-UI（最推荐方式）

```bash
VERSION=1.2.2 && bash <(curl -Ls https://raw.githubusercontent.com/alireza0/s-ui/$VERSION/install.sh) $VERSION
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


#### 检测Reality目标域名命令

```bash
======================================

for d in \
"amd.com" "aws.com" "c.6sc.co" "j.6sc.co" "b.6sc.co" "intel.com" \
"r.bing.com" "th.bing.com" "www.amd.com" "www.aws.com" "ipv6.6sc.co" \
"www.xbox.com" "www.sony.com" "rum.hlx.page" "www.bing.com" "xp.apple.com" \
"www.wowt.com" "www.apple.com" "www.intel.com" "www.tesla.com" "www.xilinx.com" \
"www.oracle.com" "www.icloud.com" "apps.apple.com" "c.marsflag.com" "www.nvidia.com" \
"snap.licdn.com" "aws.amazon.com" "drivers.amd.com" "cdn.bizibly.com" "s.go-mpulse.net" \
"tags.tiqcdn.com" "cdn.bizible.com" "ocsp2.apple.com" "cdn.userway.org" "download.amd.com" \
"d1.awsstatic.com" "s0.awsstatic.com" "mscom.demdex.net" "a0.awsstatic.com" "go.microsoft.com" \
"apps.mzstatic.com" "sisu.xboxlive.com" "www.microsoft.com" "s.mp.marsflag.com" "images.nvidia.com" \
"vs.aws.amazon.com" "c.s-microsoft.com" "statici.icloud.com" "beacon.gtv-pub.com" \
"ts4.tc.mm.bing.net" "ts3.tc.mm.bing.net" "d2c.aws.amazon.com" "ts1.tc.mm.bing.net" \
"ce.mf.marsflag.com" "d0.m.awsstatic.com" "t0.m.awsstatic.com" "ts2.tc.mm.bing.net" \
"tag.demandbase.com" "assets-www.xbox.com" "logx.optimizely.com" "azure.microsoft.com" \
"aadcdn.msftauth.net" "d.oracleinfinity.io" "assets.adobedtm.com" "lpcdn.lpsnmedia.net" \
"res-1.cdn.office.net" "is1-ssl.mzstatic.com" "electronics.sony.com" "intelcorp.scene7.com" \
"acctcdn.msftauth.net" "cdnssl.clicktale.net" "catalog.gamepass.com" "consent.trustarc.com" \
"gsp-ssl.ls.apple.com" "munchkin.marketo.net" "s.company-target.com" "cdn77.api.userway.org" \
"cua-chat-ui.tesla.com" "assets-xbxweb.xbox.com" "ds-aksb-a.akamaihd.net" "static.cloud.coveo.com" \
"api.company-target.com" "devblogs.microsoft.com" "s7mbrstream.scene7.com" "fpinit.itunes.apple.com" \
"digitalassets.tesla.com" "d.impactradius-event.com" "downloadmirror.intel.com" \
"iosapps.itunes.apple.com" "se-edge.itunes.apple.com" "publisher.liveperson.net" \
"tag-logger.demandbase.com" "services.digitaleast.mobi" "configuration.ls.apple.com" \
"gray-wowt-prod.gtv-cdn.com" "visualstudio.microsoft.com" "prod.log.shortbread.aws.dev" \
"amp-api-edge.apps.apple.com" "store-images.s-microsoft.com" "cdn-dynmedia-1.microsoft.com" \
"github.gallerycdn.vsassets.io" "prod.pa.cdn.uis.awsstatic.com" "a.b.cdn.console.awsstatic.com" \
"d3agakyjgjv5i8.cloudfront.net" "vscjava.gallerycdn.vsassets.io" "location-services-prd.tesla.com" \
"ms-vscode.gallerycdn.vsassets.io" "ms-python.gallerycdn.vsassets.io" "gray-config-prod.api.arc-cdn.net" \
"i7158c100-ds-aksb-a.akamaihd.net" "downloaddispatch.itunes.apple.com" \
"res.public.onecdn.static.microsoft" "gray.video-player.arcpublishing.com" \
"gray-config-prod.api.cdn.arcpublishing.com" "img-prod-cms-rt-microsoft-com.akamaized.net"
do
    # 记录开始时间（毫秒）
    t1=$(date +%s%3N)
    
    # 测试连接 443 端口，超时 1 秒
    if timeout 1 openssl s_client -connect "$d:443" -servername "$d" </dev/null &>/dev/null; then
        t2=$(date +%s%3N)
        echo "$d: $((t2 - t1)) ms"
    else
        echo "$d: timeout"
    fi
done
```
## 推荐代理工具
Windows/Mac（v2rayN）：https://github.com/2dust/v2rayN/releases/tag/7.12.7
Android（NekoBox）：https://github.com/MatsuriDayo/NekoBoxForAndroid/releases/tag/1.3.9
IOS/Mac（shadowrocket）：https://apps.apple.com/app/shadowrocket/id932747118



