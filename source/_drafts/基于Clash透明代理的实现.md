---
title: 基于Clash透明代理的实现
tags:
  - 教程
categories:
  - 互联网
  - 原创
mathjax: true
date: 2020-10-10 08:44:45
---
# 研究原因
为了使之前写的WireGuard大内网融合方案，能更进一步完成科学上网。而不需要在多个VPN频繁切换。目的就是实现一次接入，内网外网都可用。

# 安装与配置
## 服务端配置
Docker部署还是很香的，所以我这里使用的是Docker部署，使用官方的Docker镜像，写好一份`docker-compose.yml`配置文件,一键部署。因为Docker网络这块不太了解，所以直接使用宿主机网络，就不需要做端口映射了，也避免端口映射带来的奇怪问题。
```yml
version: '3'

services:
  clash:
    image: dreamacro/clash
    volumes:
    - ./clash:/root/.config/clash
    restart: always
    network_mode: host
    # When your system is Linux, you can use `network_mode: "host"` directly.
    container_name: clash
```
在`./clash`目录中需要准备三份文件`config.yaml``Country.mmdb``dashboard`
其中只有`config.yaml`是必须要自己编写放好。
`Country.mmdb`文件理论上Clash可以自动下载，但我尝试并不行，后来是手动下载的
`dashboard`目录用于WEB端控制的前端代码。
因为要实现透明代理，按照官方文档必须启用DNS，这里有一份`config.yaml`示例
```yml
port: 7890
socks-port: 7891
redir-port: 7892
allow-lan: true
mode: Rule
log-level: warning
external-controller: 0.0.0.0:9090
secret: ""
external-ui: dashboard
#此处内容请安装一个gui版本的clash然后在里面配置好代理然后抄过来
dns:
  enable: true
  listen: 0.0.0.0:53
  enhanced-mode: redir-host
  nameserver:
    - '114.114.114.114'
    - '223.5.5.5'
  fallback:
    - 'tls://1.1.1.1:853'
    - 'tcp://1.1.1.1:53'
    - 'tcp://208.67.222.222:443'
    - 'tls://dns.google'
proxies:
proxy-groups:
rules:
```
成功启动后接下来就是编写最为关键的`iptables`规则
为了规避流量成环问题，规则中没有对设备进行透明代理的相关代码。只有经过此电脑中转的数据包才会进行透明代理。
在此之前需要开启当前linux系统的路由功能。
```sh
iptables -t nat -N V2RAY # 新建一个名为V2RAY 的链

# Whitelist LANs and some other reserved addresses.
iptables -t nat -A V2RAY -d 0.0.0.0/8 -j RETURN
iptables -t nat -A V2RAY -d 10.0.0.0/8 -j RETURN
iptables -t nat -A V2RAY -d 127.0.0.0/8 -j RETURN
iptables -t nat -A V2RAY -d 169.254.0.0/16 -j RETURN 
iptables -t nat -A V2RAY -d 172.16.0.0/12 -j RETURN 
iptables -t nat -A V2RAY -d 192.168.0.0/16 -j RETURN 
iptables -t nat -A V2RAY -d 224.0.0.0/4 -j RETURN
iptables -t nat -A V2RAY -d 240.0.0.0/4 -j RETURN

# whitelist China ip.
#iptables -t nat -A V2RAY -p tcp -m set --match-set china dst -j RETURN

iptables -t nat -A V2RAY -p tcp -j RETURN -m mark --mark 0xff # 此规则目的是避免代理本机流量出现回环问题
iptables -t nat -A V2RAY -p tcp -s 192.168.88.0/24 ! -d 192.168.88.0/24 -j REDIRECT --to-ports 7892 # 指定CIDR地址流量转发7892端口
iptables -t nat -A V2RAY -p tcp -s 192.168.10.0/23 ! -d 192.168.10.0/23 -j REDIRECT --to-ports 7892 # 指定CIDR地址流量转发7892端口

iptables -t nat -A PREROUTING -p tcp -j V2RAY # 对局域网其他设备进行透明代理
#iptables -t nat -A OUTPUT -p tcp -j V2RAY # 对本机进行透明代理
```
配置好后可以观察能否进行透明代理。
通过在本机访问http://localhost:9090/ui/可以使用WEB管理Clash
通过使用`docker-compose logs`可查看Clash运行日志
测试没问题后，需要将iptables规则保存，在下次自启动时，能自动生效。
[Ubuntu Server 如何永久儲存iptables的設定？](https://magiclen.org/ubuntu-server-iptables-save-permanently/)

## 客户端配置
在一个局域网环境下(二层网络中),将设备网关与DNS均指向上述部署了Clash的linux机子中即可使用。
除此之外还可以通过DHCP来下发代理网关和DNS，也可以通过DHCP来指定需要设备下发，其余设备走默认网关/DNS。
`DHCP Options 6 DNS`
`DHCP Options 3 Gateway`
指定Options即可。
除此之外，DHCP还可以下发PAC地址，客户端自动配置代理。目前测试Windows，IOS均可使用，Android，Linux不太行。
`DHCP Options 252 PAC`
Windows IOS均需要启用代理自动获取

# 与WireGuard联动
在相同的机子部署WireGuard，并设置这台电脑为出口网关，其余设备只要接入WireGuard，就既能访问WireGuard设备中的内网资源，又能完成科学上网。
如果你的机子与部署WireGuard的服务器位于同一局域网（二层网络中），通过修改网关即可接入，不需要再挂Wireguard VPN。