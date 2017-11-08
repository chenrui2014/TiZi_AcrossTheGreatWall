## 安装瑞速
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