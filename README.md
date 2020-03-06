# Padavan-build
🍴 自 [chongshengB/Padavan-build](https://github.com/chongshengB/Padavan-build)。

- 利用 Github Action 自动编译 K2P 固件，每周五凌晨编译，并输出为 [Release](https://github.com/rosuH/Padavan-build/releases)
- 仅保留 [SmartDNS](https://github.com/pymumu/smartdns/issues)，固件大小为 7M 左右，适合什么都不要的用户使用。

## 附上 SmartDns 配置

如果使用 SmartDNS 解析国外域名，有可能返回和你国外节点相去甚远的 IP 地址，导致访问变得更加缓慢。参见[加入 SmartDNS 其实主要是用...](https://github.com/coolsnowwolf/lede/issues/2551)。如果你不想折腾的话，建议使用 HK 或相近的结点。

### DNS列表

UI 界面直接设置即可。

- 深圳电信: 202.96.134.133
- 阿里 DNS: 223.5.5.5
- DNSPod: 119.29.29.29
- Google: 8.8.8.8 
- 114DNS: 114.114.114.114 
- OpenDNS: 208.67.220.220
- CNNIC: 1.2.4.8
- DNS.sb-HTTPS: 185.222.222.222@853 

ref:
- [dns list](https://www.ip.cn/dns.html)

`cat /etc/storage/smartdns.conf`:

```conf
server-name smartdns
bind :6053
cache-size 4096
prefetch-domain yes
serve-expired no
log-level info
server 223.5.5.5
server 119.29.29.29
server 114.114.114.114
server 208.67.220.220
server 1.2.4.8
server 202.96.134.133
server-tls 185.222.222.222:853 
# Add domains which you want to force to an IP address here.
# The example below send any host in example.com to a local webserver.
# address /domain/[ip|-|-4|-6|#|#4|#6]
# address /www.example.com/1.2.3.4, return ip 1.2.3.4 to client
# address /www.example.com/-, ignore address, query from upstream, suffix 4, for ipv4, 6 for ipv6, none for all
# address /www.example.com/#, return SOA to client, suffix 4, for ipv4, 6 for ipv6, none for all

# specific ipset to domain
# ipset /domain/[ipset|-]
# ipset /www.example.com/block, set ipset with ipset name of block 
# ipset /www.example.com/-, ignore this domain

# specific nameserver to domain
# nameserver /domain/[group|-]
# nameserver /www.example.com/office, Set the domain name to use the appropriate server group.
# nameserver /www.example.com/-, ignore this domain
# Add IP blacklist which you want to filtering from some DNS server here.
# The example below filtering ip from the result of DNS server which is configured with -blacklist-ip.
# blacklist-ip [ip/subnet]
# blacklist-ip 254.0.0.1/16
# Add IP whitelist which you want to filtering from some DNS server here.
# The example below filtering ip from the result of DNS server which is configured with -whitelist-ip.
# whitelist-ip [ip/subnet]
# whitelist-ip 254.0.0.1/16
# Add custom settings here.

# set log level
# log-level [level], level=fatal, error, warn, notice, info, debug
# log-level error

# log-size k,m,g
# log-size 128k

# log-file /var/log/smartdns.log
# log-num 2

# List of hosts that supply bogus NX domain results 
# bogus-nxdomain [ip/subnet]

```

