* <h3>nginx linux环境下安装</h3>
	* 下载相关组件
		* wget http://nginx.org/download/nginx-1.10.2.tar.gz
		* wget http://www.openssl.org/source/openssl-fips-2.0.10.tar.gz
		* wget http://zlib.net/zlib-1.2.11.tar.gz
		* wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.40.tar.gz <br></br>
	* 安装c++编译环境，如已安装可略过
		* yum install gcc-c++
		* Is this ok [y/N]:y<br></br>
	* 安装Nginx及相关组件
	* openssl安装 (配置https需要的)
		* tar zxvf openssl-fips-2.0.10.tar.gz
		* cd openssl-fips-2.0.10
		* ./config && make && make install<br></br>
	
	* pcre安装(正则相关)
		* tar zxvf pcre-8.40.tar.gz
		* cd pcre-8.40
		* ./configure && make && make install<br></br>
		
	* zlib安装（数据压缩）
		* tar zxvf zlib-1.2.11.tar.gz
		* cd zlib-1.2.11
		* ./configure && make && make install<br></br>
	* nginx安装
		* tar zxvf nginx-1.10.2.tar.gz
		* cd nginx-1.10.2
		* ./configure && make && make install <br></br>
	* 启动Nginx
		* 找到nginx安装在什么位置 whereis nginx
		* 进入目录启动 ./nginx
		* 报错 error while loading shared libraries: libpcre.so.1: cannot open shared object file: No such file or directory
		* 解决 whereis libpcre.so.1命令找到libpcre.so.1在哪里
		* 2.用ln -s /usr/local/lib/libpcre.so.1 /lib64命令做个软连接就可以了
		* 3.用sbin/nginx启动Nginx
		* 4.用ps -aux | grep nginx查看状态
* <h3>nginx基本操作</h3>
	* 启动nginx
		* ./nginx
	* 停止
		* ./nginx -s stop  
	* 重启
		* ./nginx -s reload
	* 命令帮助
		* ./nginx -h
	* 配置文件
		* nginx.conf
	* 验证配置文件
		* .nginx -t
* <h3>开启外网访问</h3>
	* 在Linux系统中默认有防火墙Iptables管理者所有的端口，只启用默认远程连接22端口其他都关闭，咱们上面设置的80等等也是关闭的，所以我们需要先把应用的端口开启
		* 方法一直接关闭防火墙，这样性能较好，但安全性较差，如果有前置防火墙可以采取这种方式
			*  serviceiptables stop
			* chkconfig iptables off
			* chkconfig --list|grep ipt
		* 方法二将开启的端口加入防火墙白名单中，这种方式较安全但性能也相对较差
			* 编辑防火墙白名单 vim /etc/sysconfig/iptables
			* 增加下面一行代码 -A INPUT -p tcp -m state -- state NEW -m tcp --dport 80 -j ACCEPT
			* 保存退出，重启防火墙 service iptables restart
* 
				