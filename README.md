# 科学上网的秘籍
> 如果有更好的教程，欢迎大佬们提`issue`
* 欢迎去Download文件夹下载ssr，proxifier，openvpn客户端
* 这篇教程稍难，但是效果是所有教程中最好的，如果您没用太多经验，可能会遇到些问题
* 旧版本教程链接（方法笨些，解释更友好些） [请点这里](https://github.com/XetRAHF/TiZi_AcrossTheGreatWall/blob/master/README-dept.md)

[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/dwyl/esta/issues)

## 关于喝茶
* 仅供科学研究使用
* 如果喜欢就`follow`我吧，多谢🙏
* 请不要在`issue`里面谈论`政治`
* 如果文章里面的链接失效，请`issue`
* 如果我被请去喝茶了，请`fork`走
![滑稽](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1509657102720&di=26897a14c32e3b7125d72a9ee4a6571f&imgtype=0&src=http%3A%2F%2Fimg.alicdn.com%2Fimgextra%2Fi2%2F2242406473%2FTB2o2RgahvC11Bjy1zdXXXPcVXa_%2521%25212242406473.jpg)

## 致谢
* Shadowsocks 和 ShadowsocksR作者
![Shadowsock Logo](https://raw.githubusercontent.com/XetRAHF/TiZi_AcrossTheGreatWall/d1f812d0caabe9c0d4a4b7d9e456ef46671f2729/imgs/shadowsocks.png)
* 所有参与编写的志愿者

## 选翻墙服务器
* 不要使用基于OpenVZ虚拟化技术的服务器
* 点这里看[国外知名提供商的比较](https://github.com/joedicastro/vps-comparison)

## 买翻墙服务器
* 你需要一张信用卡（如果你没有你可以使用`Global cash全球付`, 或者使用汇率飞起的淘宝虚拟信用卡）
* 你需要为每个月准备至少5美元，或10美元（已经很低了，减减肥，就省出来了）

## 快速部署纽约shadowsocks-r服务器（10-15分钟）
### 启动服务器
* 推荐配置
	* CPU：一个核心足以
	* 内存：512即可
	* 硬盘：10G以上即可
	* 推荐系统：CentOS 6 x64

### 启用 Google BBR - Cent OS 版本
* 请参考VULTR官方教程 [链接](https://www.vultr.com/docs/how-to-deploy-google-bbr-on-centos-7)
* 若上述链接出现问题，这里有一份命令备份 [链接](https://bitbucket.org/xetrafhan/anti-gfw/src/8131926257e405e494a119130e68fccff840b73f/install-bbr-cent-7-64.md?at=master&fileviewer=file-view-default)

### 启用 Google BBR - Ubuntu 版本
* 请使用下面的命令
```bash
apt-get update && wget --no-check-certificate -qO 'bbr-on-ubuntu-16.sh' 'https://bitbucket.org/xetrafhan/anti-gfw/raw/3ebcd6b971100bdb0967201e8da067df7f7e171d/install-bbr-on-ubuntu-16.sh' && chmod a+x bbr-on-ubuntu-16.sh && bash bbr-on-ubuntu-16.sh -f
```

### 编译安装SSR
* 请使用下面的命令
```bash
yum update -y && yum install -y wget net-tools vim && wget https://bitbucket.org/xetrafhan/anti-gfw/raw/b95df58520e5c5579c780a1633b3537a362383a9/shadowsocks-all.sh && bash ./shadowsocks-all.sh
```

### 配置示范（工作使用）
| key | value | 
|----|------|
| 密码 | wpoipgepa123 | 
| Encryption | aes-256-cfb | 
| Protocol | auth_aes128_sha1 | 
| Obfs | tls1.2_ticket_auth | 
| port | 8989 | 

### 配置示范（游戏使用）
| key | value | 
|----|------|
| 密码 | wpoipgepa123 | 
| Encryption | chacha20 | 
| Protocol | origin | 
| Obfs |  http_simple | 
| port | 8989 | 

### 启动TCP Fast Open
* 执行命令
```bash
echo 3 > /proc/sys/net/ipv4/tcp_fastopen
```
* 在`/etc/sysctl.conf`文件中加入(如果您使用*Vim*，直接按`O`键添加)
```java
net.ipv4.tcp_fastopen = 3
```


### 修改启动命令
* 修改`/etc/rc.local`文件,(如果您使用CentOS 7，请Google一下如何启用rc.local启动命令，如果您使用Ubuntu，请使用`systemctl enable rc-local.service`启用`rc.local`)
```bash
echo 3 > /proc/sys/net/ipv4/tcp_fastopen
/etc/init.d/shadowsocks-r restart
```

### 修改Shadowsocks配置
* 修改`/etc/shadowsocks-r/config.json`文件，开启ipv6，TCP Fast Open，延长Timeout时间，这里提供一个示例
```json
{
    "server":"0.0.0.0",
    "server_ipv6":"::",
    "server_port":8989,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"wpoipgepa123",
    "timeout":120,
    "method":"chacha20",
    "protocol":"origin",
    "protocol_param":"",
    "obfs":"http_simple",
    "obfs_param":"",
    "redirect":"",
    "dns_ipv6":true,
    "fast_open":true,
    "workers":1
}
```

### 重新启动ssr
* 执行命令
```bash
/etc/init.d/shadowsocks-r restart
```

## 快速部署硅谷转发服务器(1-2分钟)
### 同样的服务器配置， 按照上述教程开启BBR 
### 配置iptables
* 替换$FORWARDPORT为443或80
* 替换$TARGETIP为纽约服务器的地址
* 替换$TARGETPORT为8989
* 替换$LOCALIP为硅谷服务器的地址
* 然后执行命令
```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A PREROUTING -p tcp --dport $FORWARDPORT -j DNAT --to-destination $TARGETIP:$TARGETPORT
iptables -t nat -A POSTROUTING -p tcp -d $TARGETIP --dport $FORWARDPORT -j SNAT --to-source $LOCALIP
```

### 关闭服务器ping与ssh功能
```bash
echo 1 >/proc/sys/net/ipv4/icmp_echo_ignore_all
sudo iptables -A INPUT -p tcp --dport 22 -j DROP
```

## 配置客户端
* 几点提示
* 服务器ip填写硅谷服务器ip
* 服务器port填写443
* UDP Forwarding不支持
* 根据您的情况开启或关闭ipv6
* 配置proxifier，并在proxifier的设置中开启系统进程以及root系统服务代理（这个功能非常重要，但是需要手动开启, 开启后proxifier能捕捉所有命令行应用，实现全局代理），关闭Handle Direct Conenction

## 关于原理
* 请求被Proxifier转发到shadowsocks-r客户端，随后被转发到硅谷服务器，然后硅谷服务器转发该请求到纽约服务器。

## 这样做的好处
* 百度一下，你的ip显示为纽约的服务器ip，这样硅谷服务器的ip就被隐藏了起来。（TCP Relay）
* 修复成本低
* 如果您的vps提供商支持一机多IP功能，您也可以使用该功能来做TCP Relay
* 您还可以在vps设置中修改服务器的反向dns解析到github.com等知名域名

## 其他
* 如果您的服务器在日本，您可以通过更改`/etc/sysconfig/network-scripts/ifcfg-eth0`DNS设置，然后使用`/etc/init.d/network restart`应用更改
* 如果您只使用代理，请看[旧版本教程](https://github.com/XetRAHF/TiZi_AcrossTheGreatWall/blob/master/README-dept.md)，里面有代理配置说明
* windows中torrent与dropbox依然存在问题，不能使用
* Proxifier for mac 激活码：P427L-9Y552-5433E-8DSR3-58Z68 
* Proxifier for windows: KFZUS-F3JGV-T95Y7-BXGAS-5NHHP 


## 谁都不会告诉你的秘密
* 搭建稳定翻墙服务器的核心秘诀是选择一个优质的服务器地理位置，和下行速度快的服务器
