# 科学上网的秘籍
> 还在努力编写中, 欢迎大家一起来帮忙，在development分支继续开发
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/dwyl/esta/issues)

> 如果您熟悉linux系统，您可以使用更先进的ssr串联服务器架构，该方法更稳定(支持ip混淆同时支持故障重启)，但部属过程复杂，[点进来看readme.md](https://zerqqr1_xetrastudio@bitbucket.org/xetrafhan/anti-gfw.git)

## 关于喝茶
* 如果喜欢就`follow`我吧，多谢🙏
* 请不要在`issue`里面谈论`政治`
* 如果您对认为文章有(malicious suspect)，请`issue`通知我
* 如果文章里面的链接失效，请`issue`
* 如果我被请去喝茶了，请`fork`走
![滑稽](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1509657102720&di=26897a14c32e3b7125d72a9ee4a6571f&imgtype=0&src=http%3A%2F%2Fimg.alicdn.com%2Fimgextra%2Fi2%2F2242406473%2FTB2o2RgahvC11Bjy1zdXXXPcVXa_%2521%25212242406473.jpg)

## 致谢
* Shadowsocks 和 ShadowsocksR作者
![Shadowsock Logo](https://raw.githubusercontent.com/XetRAHF/TiZi_AcrossTheGreatWall/d1f812d0caabe9c0d4a4b7d9e456ef46671f2729/imgs/shadowsocks.png)
* 所有参与编写的志愿者

## 选翻墙服务器
* 不要选择基于OpenVZ内核的服务器提供商（瑞速不支持这个）（当然如果您听不懂可以忽略掉）
* 首推三家知名服务商：
	* DigitalOcean: `https://www.digitalocean.com/`
	* Vultr: `https://www.vultr.com`
	* Linode: `https://www.linode.com`

* 然后是日本的服务商：
	* 维基百科地址： `https://romanrm.net/vps/japan`

* 美国的服务商：
	* CloudWays: `www.cloudways.com`

## 买翻墙服务器
* 你需要一张信用卡（如果你没有你可以使用`Global cash全球付`, 或者使用汇率飞起的淘宝虚拟信用卡）
* 你需要为每个月准备至少5美元，或10美元（已经很低了，减减肥，就省出来了）

## 配置翻墙服务器
### 启动服务器
* 推荐配置
	* CPU：一个核心足以
	* 内存：512即可
	* 硬盘：10G以上即可
	* 推荐系统：CentOS 6 x64
	* 推荐内核(kernel)版本：4.4.0-x86-64
* 示范例子1:
	* 环境（Linode新加坡）
	* 选择服务器
	![Choose Server]()
### 更换服务器内核 (重要步骤)
```
wget http://ftp.scientificlinux.org/linux/scientific/6.6/x86_64/updates/security/kernel-2.6.32-504.3.3.el6.x86_64.rpm
rpm -ivh kernel-2.6.32-504.3.3.el6.x86_64.rpm --force
reboot
```

* 示范例子1:
* 环境（Linode新加坡）

### 安装瑞速
* 为什么：这个东西能使你原本与服务器连接只有300KBs的速度提升到60M以上
* 怎么做：
```
wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeser_Install/master/appex.sh && chmod +x appex.sh && bash appex.sh install
```
软件会询问你一些事情，全部选择y
* 原理是什么：[TCP抗堵塞原理](https://cloudplatform.googleblog.com/2017/07/TCP-BBR-congestion-control-comes-to-GCP-your-Internet-just-got-faster.html)
* 更多文献：
	* 瑞速库地址：https://github.com/91yun/serverspeeder
* (高手专用)
	* 您当然也可以使用google bbr，但是根据我们的测试，使用瑞速更稳定，如果您选择使用BBR而不是瑞速那么请参考下列文章
		* [Vultr官方：在CentOS上安装Google BBR](https://www.vultr.com/docs/how-to-deploy-google-bbr-on-centos-7)

	
### 启动瑞速
```
/appex/bin/serverSpeeder.sh restart
```

### 安装Docker
* 为什么：
	* 我们需要运行两个SSR容器，这样我们就可以有两个服务器端口用作SSR服务
	* 不建议使用docker的shadowsocksr镜像
	
* 怎么做：
```
rpm -iUvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
yum update -y
yum -y install docker-io
service docker start
```
### 部署两个Docker SSR容器
* 启动第一个SSR容器并开启SSR服务

```
docker run --name shadowsock1 -p 443:8989 -ti centos:6 /bin/bash
```
* 在容器内执行

```
  yum update -y && yum install -y wget net-tools vim && wget https://raw.githubusercontent.com/xetra-enterprize/shadowsocks_install/master/shadowsocks-all.sh && bash ./shadowsocks-all.sh
```
* 用vim编辑器编辑/etc/rc.local

```
vi /etc/rc.local 
```
* 在这个文件的末尾追加
 
```
echo 3 > /proc/sys/net/ipv4/tcp_fastopen
```
* 用vim编辑器编辑/etc/sysctl.conf

```
vi /etc/sysctl.conf
```
* 在这个文件的末尾追加

```
net.ipv4.tcp_fastopen = 3
```

* 用vim编辑器编辑/etc/shadowsocks-r/config.json

```
vi /etc/shadowsocks-r/config.json
```
* 里面有个`tcp_fast_open`的变量，把false改成true

* 最后重启SSR服务

```
/etc/init.d/shadowsocks-r restart
```
* 使用`Ctrl+D`退出容器

* 启动第二个SSR容器并开启SSR服务

```
docker run --name shadowsock2 -p 80:8989 -ti centos:6 /bin/bash
```
* 在容器内执行

```
  yum update -y && yum install -y wget net-tools vim && wget https://raw.githubusercontent.com/xetra-enterprize/shadowsocks_install/master/shadowsocks-all.sh && bash ./shadowsocks-all.sh
```
* 用vim编辑器编辑/etc/rc.local

```
vi /etc/rc.local 
```
* 在这个文件的末尾追加
 
```
echo 3 > /proc/sys/net/ipv4/tcp_fastopen
```
* 用vim编辑器编辑/etc/sysctl.conf

```
vi /etc/sysctl.conf
```
* 在这个文件的末尾追加

```
net.ipv4.tcp_fastopen = 3
```

* 用vim编辑器编辑/etc/shadowsocks-r/config.json

```
vi /etc/shadowsocks-r/config.json
```
* 里面有个tcp_fast_open的变量，把false改成true

* 最后重启SSR服务

```
/etc/init.d/shadowsocks-r restart
```
* 使用`Ctrl+D`退出容器
* 至此我们就完成了服务器的配置


* 示范例子1：
* 环境(Linode新加坡机房):



### 保证服务器稳定性
* 你需要至少两个服务器，才能保证你的上网体验
* 所以再部署一个服务器吧
* 不要认为给一个服务器上加两个ip地址就可以了，防火长城进行封锁会导致整个区域断线，而不只是你的ip断线。所以你应该换一个地区创建第二个服务器。
* （高手专用）因为shadowsocks支持监听服务器所有地址（VPN不支持）所以你可以给服务器做一个快照（如果到这里你还读不懂的话，就忽略掉吧），然后再第二个服务器山复原快照，但是你仍然需要为第二个服务器手动更换内核，安装瑞速，启动容器，并进入每一个Docker容器开启SSR服务

## 配置翻墙服务器防火墙（高手装用，非必需）
* 只开放80和443端口，避免被ping到



# 服务器配置好了，我们现在在电脑上配置全局翻墙
## 手机
* 从ishadow下载(这里是ishadow的官网：`https://ss.ishadowx.net`)：
	* 安卓版本：`http://160.16.231.71/ssr-3.3.5.apk`
	* IOS版本：`http://dwz.cn/5vCPvz`
* 从本库下载：
	* 安卓版本：`https://github.com/XetRAHF/TiZi_AcrossTheGreatWall/blob/91e5f3d04afcf72db83781d9a6be22dbe50b68a4/ssr-3.3.5.apk?raw=true`
* （高手专用）这里是shadowsocksR的源码：
	`https://github.com/shadowsocksr-backup/shadowsocksr`
* （高手专用）这里有shadowsocks的全家桶：
	`https://github.com/teddysun/shadowsocks_install`

	
## 个人PC与Mac
### 安装ShadowsocksR客户端
* 从ishadow下载(这里是ishadow的官网：`https://ss.ishadowx.net`)：
	* Mac版本：`http://160.16.231.71/SSX-NG-R8.dmg`
	* Windows版本：`http://160.16.231.71/ssr-4.1.4-win.7z`
* 从本库下载
	* Mac版本：`https://github.com/XetRAHF/TiZi_AcrossTheGreatWall/blob/91e5f3d04afcf72db83781d9a6be22dbe50b68a4/SSX-NG-R8.dmg?raw=true`
	* Windows版本：`https://github.com/XetRAHF/TiZi_AcrossTheGreatWall/blob/91e5f3d04afcf72db83781d9a6be22dbe50b68a4/ssr-4.1.4-win.zip?raw=true`

# 用Proxifier将我们的ShadowsocksR转换为VPN模式
> 此时ShadowsocksR就和VPN一样了
## Proxifier 官网

* Proxifier for mac 激活码：P427L-9Y552-5433E-8DSR3-58Z68 
* Proxifier for windows: KFZUS-F3JGV-T95Y7-BXGAS-5NHHP 

[Proxifier(把你的shadowsocksR转换成为VPN)](https://www.proxifier.com)

### 给常用的程序上代理（程序员）
* Docker 使用国内镜像：
* 修改Docker配置文件`/etc/default/docker`如下：
  `DOCKER_OPTS="--registry-mirror=http://aad0405c.m.daocloud.io"`
  使用`service docker restart`重启`Docker服务`即可。
> 如果您使用proxifier最好也还是再配置代理，那样会更稳

* GIT:
	*  `git config --global http.proxy 'socks5://127.0.0.1:1086'`

* Node Package Manager(NPM)（请看文章末尾）:

```
npm config set strict-ssl false
npm config set proxy http://127.0.0.1:1087
npm config set https-proxy http://127.0.0.1:1087
export HTTP_PROXY=http://127.0.0.1:1087
export HTTPS_PROXY=http://127.0.0.1:1087
env http_proxy=http://127.0.0.1:1087
```

* SSH(Tested on Mac OS):
	* `ssh root@128.384.23.32 -o "ProxyCommand=nc -X 5 -x 127.0.0.1:1086 %h %p`
	* `ssh root@目标ip -o "ProxyCommand=nc -X 5 -x 127.0.0.1:1086 %h %p`
* Homebrew:
	* `export ALL_PROXY="127.0.0.1:1087"`
* Cocoapods:
	* Cocoapods基于Git与curl(系统代理设置)，你需要给git上代理然后
	```
	export HTTP_PROXY=http://127.0.0.1:1087
	export HTTPS_PROXY=http://127.0.0.1:1087
	env http_proxy=http://127.0.0.1:1087
	```
* PyPi: 
```
export HTTP_PROXY=http://127.0.0.1:1087
export HTTPS_PROXY=http://127.0.0.1:1087

sudo pip --proxy http://PROXYDOM:PROXYPORT install package
```


## 为什么这样做是最好的翻墙方案：
* 为什么不使用VPN：
	* PPTP: 约1～2小时即可被防火长城检测出来，然后ip无法访问
	* L2tp: 成熟的配置库非常少，连接不稳定
	* IPsec: 编译时间长，会被检测出来同时被限速
	* 总结： 以上三种方法都有一个巨大的缺点，端口是固定的，流量特征明显，速度缓慢，连接容易断线

* 为什么不使用SS（注意不是SSR）：
	* 某大学学生发文使用深度学习方法学习了SS流量特征，可以很精确检测出来SS并进行限速，论文地址如下：`https://github.com/shadowsocks/shadowsocks/issues/540`

* 为什么不使用XX-Net（`https://github.com/XX-net/XX-Net`）：
	* 无法扫描ip
	* 速度慢
	* 每隔1分钟ip就会被切换一次，导致连接中断
	* 每个谷歌账号最多12G左右流量
	* 需要谷歌账号，并激活
	* 部署ip速度慢
	
* 为什么不使用OpenVPN（TCP与UDP）：
	* 速度慢
	* 服务器部署时证书生成速度慢
	* 即使是TCP版本，同样会被检测出来同时被防火长城限速
	* Mac客户端Tunnelblick收费
	* 经测试使用TCP版本时（Tunnelblick）无法播放youtube视频

* 为什么不使用蓝灯（`https://github.com/getlantern/lantern`）:
	* 速度慢
	* 免费版本已经在大多数地区无法使用

* 为什么不使用expressVPN(`https://www.expressvpn.com/`)
	* 高昂的价格
	* 速度慢

## 几件一定不要去做的事：
* 省钱：翻墙工具每个月花费70块钱左右是最好的，也就一天的饭钱，花吧，值得来。
* 使用国内云服务器翻墙：（例如： 阿里云， 京东云等）（阿里云国际版的服务条款已经写到如果用户用来搭建互联网穿透服务，封号并禁用你的VISA卡）
* 使用国内聊天工具(如QQ群)将服务器信息分享给好友：（自然语言处理器会检测出来的）
* 使用QQ群分享服务器给好朋友：（同学，qq群不算用户隐私，会被查的）
* 只搭建一个梯子服务器：即使你的服务器是SSR加密等级非常高，甚至是嵌套SSR，你也需要准备两个以上的梯子服务器，因为出口线路也会发生不稳定的情况
* 卖SSR以及其他翻墙服务器：（后果极为严重，请大家不要尝试）`http://www.ajxxgk.jcy.cn/html/20170419/2/5261188.html`
* 不要在Azure中国（由世纪互联运营）上搭建翻墙服务器，会被查水表
* 不要使用AWS和Google Cloud等(Pay as you Go)的服务器提供商上搭建梯子（当然，如果您是土豪的话是可以的）那里的流量是按照GB计费的，非常贵

## 关于串联服务器的误区
* 你可能认为设置一个日本的服务器，再设置一个美国的服务器，让日本的服务器做中转，这样就就可以加快连接的速度，降低延迟。如果美国服务器没有被GFW限速或禁止，那么这样做只会使你的速度更慢。

## 谁都不会告诉你的秘密
* 搭建稳定翻墙服务器的核心秘诀是选择一个优质的服务器地理位置

## 原理问题：
* Shadowsocks与VPN之间的关系：
	* 参考：[Shadowsocks与VPN的区别](http://blog.csdn.net/guyue35/article/details/50932177)

* Shadowsocks与ShadowsocksR的关系：
	* 参考：[Shadowsocks与ShadowsocksR的关系](https://www.librehat.com/about-shadowsocks-r-and-the-security-of-shadowsocks/)

## 我们可以让日本服务器转发我们的连接到美国服务器, 下面就是一个例子
```
sudo su
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A PREROUTING -p tcp --dport 8388 -j DNAT --to-destination US_VPS_IP:8388
iptables -t nat -A POSTROUTING -p tcp -d US_VPS_IP --dport 8388 -j SNAT --to-source JAPAN_VPS_IP
```
## 让服务器只接受443端口
```
 iptables -t filter -m owner --uid-owner ssuser -A OUTPUT -p tcp --dport 443 -j ACCEPT
 iptables -t filter -m owner --uid-owner ssuser -A OUTPUT -p tcp -j REJECT --reject-with tcp-reset
```

## 基于OpenWRT的路由器
> 推荐架构


## 最后祝大家办公愉快

## 鉴于npm不能使用代理的问题
安装OpenVPN服务器
```
wget https://raw.githubusercontent.com/Angristan/OpenVPN-install/master/openvpn-install.sh
chmod +x openvpn-install.sh
```
配置乌班图客户端
```
sudo apt-get install openvpn
sudo apt-get install network-manager-openvpn-gnome
sudo openvpn --config '/home/jglerner/Desktop/vpnbook-us1-tcp443.ovpn'
```


···
docker exec -ti e763b2ab011a /bin/bash
docker exec -ti 944b08625cec /bin/bash
docker exec -ti 6c5427f92cb1 /bin/bash
docker exec -ti bc6b9971acbe /bin/bash
 ```
