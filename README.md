# 科学上网的最终秘籍（最详细的说明）
> 还在努力编写中, 欢迎大家一起来帮忙
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/dwyl/esta/issues)
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





// Development ---------------------
## 配置翻墙服务器
### 启动服务器

* 示范例子1:
	* 环境（Linode新加坡）
	* 选择服务器
	![Choose Server]()


* 示范例子1:
* 环境（Linode新加坡）

### 安装瑞速


	


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
* 怎么做：
```
docker run --name shadowsock1 -p 443:8989 -ti centos:6 /bin/bash
docker run --name shadowsock2 -p 80:8989 -ti centos:6 /bin/bash
```
### 安装并启动两个SSR容器
* 使用`docker ps -a`查看你的`containerID`
* 分别启动2个容器并配置ssr服务

* 示范例子1：
* 环境(Linode新加坡机房):



### 保证服务器稳定性


## 配置翻墙服务器防火墙（高手装用，非必需）



# 服务器配置好了，在个人电脑上配置全局翻墙


# 用Proxifier将我们的ShadowsocksR转换为VPN模式


### 给常用的程序上代理（程序员）



## 为什么这样做是最好的翻墙方案：


## 几件一定不要去做的事：


## 原理问题：



## 基于OpenWRT的路由器
> 推荐架构


## 最后祝大家办公愉快
```
Severspeeder:
        wget http://ftp.scientificlinux.org/linux/scientific/6.6/x86_64/updates/security/kernel-2.6.32-504.3.3.el6.x86_64.rpm
        rpm -ivh kernel-2.6.32-504.3.3.el6.x86_64.rpm --force
        reboot

        wget --no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeser_Install/master/appex.sh && chmod +x appex.sh && bash appex.sh install
        /appex/bin/serverSpeeder.sh restart
        yyy

    Linode VPS as a VPN:
        System: CentOS 6 x64
        change kernel version to 4.4.0-x86-64-linode63

        rpm -iUvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
        yum update -y
        yum -y install docker-io
        service docker start

        docker run --name shadowsock1 -p 443:8989 -ti centos:6 /bin/bash
            yum update -y && yum install -y wget net-tools vim && wget https://raw.githubusercontent.com/xetra-enterprize/shadowsocks_install/master/shadowsocks-all.sh && bash ./shadowsocks-all.sh
            vi /etc/rc.local 
            > Appending following lines to the end of file:
                echo 3 > /proc/sys/net/ipv4/tcp_fastopen
            
            vi /etc/sysctl.conf
            > Appending following lines to the end of file:
                net.ipv4.tcp_fastopen = 3
            
            vi /etc/shadowsocks-r/config.json
            > Change to true enable fast open

            /etc/init.d/shadowsocks-r restart
        
        docker run --name shadowsock2 -p 80:8989 -ti centos:6 /bin/bash
            yum update -y && yum install -y wget net-tools vim && wget https://raw.githubusercontent.com/xetra-enterprize/shadowsocks_install/master/shadowsocks-all.sh && bash ./shadowsocks-all.sh
            vi /etc/rc.local 
            > Appending following lines to the end of file:
                echo 3 > /proc/sys/net/ipv4/tcp_fastopen
            
            vi /etc/sysctl.conf
            > Appending following lines to the end of file:
                net.ipv4.tcp_fastopen = 3
            
            vi /etc/shadowsocks-r/config.json
            > Change to true enable fast open

            /etc/init.d/shadowsocks-r restart

        
    Test it before use it!
        docker exec -ti e763b2ab011a /bin/bash
        docker exec -ti 944b08625cec /bin/bash
        docker exec -ti 6c5427f92cb1 /bin/bash
        docker exec -ti bc6b9971acbe /bin/bash
 ```
