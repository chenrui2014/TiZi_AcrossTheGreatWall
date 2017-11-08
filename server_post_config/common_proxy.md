### 给常用的程序上代理（程序员）
> 如果您使用proxifier最好也还是再配置代理，那样会更稳

* GIT:
	*  `git config --global http.proxy 'socks5://127.0.0.1:1086'`

* Node Package Manager(NPM):

```
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