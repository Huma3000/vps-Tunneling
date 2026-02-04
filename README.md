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






