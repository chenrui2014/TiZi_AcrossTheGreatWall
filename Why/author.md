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