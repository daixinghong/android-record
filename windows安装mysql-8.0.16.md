* 下载mysql-8.0.16
	* ![](https://i.imgur.com/r25CArd.png)
* 下载完成后解压
	* ![](https://i.imgur.com/pEDd2J6.png)
* 进入该文件夹
	* ![](https://i.imgur.com/Cn73USO.png)
* 新建my.ini文件，内容复制下面内容
	<pre class="prettyprint lang-javascript">
	[mysqld]
	 #设置3306端口
	port=3306
	 # 设置mysql的安装目录
	basedir=D:\Program Files\MySQL
	 # 设置mysql数据库的数据的存放目录
	datadir=D:\Program Files\MySQL\Data
	 # 允许最大连接数
	max_connections=200
	 # 允许连接失败的次数。
	max_connect_errors=10
	 # 服务端使用的字符集默认为utf8mb4
	character-set-server=utf8mb4
	 # 创建新表时将使用的默认存储引擎
	default-storage-engine=INNODB
	 # 默认使用“mysql_native_password”插件认证
	 #mysql_native_password
	default_authentication_plugin=mysql_native_password
	[mysql]
	 # 设置mysql客户端默认字符集
	default-character-set=utf8mb4
	[client]
	 # 设置mysql客户端连接服务端时默认使用的端口
	port=3306
	default-character-set=utf8mb4

</pre> 

* 配置环境变量
	* ![](https://i.imgur.com/1tFUqyc.png)

* 打开命令行，用管理员权限打开，然后cd到mysql安装路径bin目录
	* ![](https://i.imgur.com/YDVhFj9.png)
	
	* ![](https://i.imgur.com/goDBqyP.png)
* 执行命令: mysqld --initialize --console ，红色框内是数据库初始密码，保存起来，修改密码时需要用
	* ![](https://i.imgur.com/tRnjXBx.png)
* 安装mysql服务，执行命令：mysqld --install
	 ![](https://i.imgur.com/S1nAR3n.png)
	* 如果出现下面这个情况，说明mysql服务已经存在
		 * ![](https://i.imgur.com/tp6vZMW.png)
	* 使用命令:sc delete mysql  出现如下图说明删除成功
		 * ![](https://i.imgur.com/hWjPKBO.png)
	* 再执行安装服务命令: mysqld --install  出现如下图则安装成功
		 * ![](https://i.imgur.com/Z7YGvAX.png)

* 启动mysql数据库服务
	* 执行命令:net start mysql  出现如下图则启动成功
		 * ![](https://i.imgur.com/q6b30oP.png)
* 连接数据库 使用navicat工具 账号:root  密码就是最开始初始化时的初始密码
	 ![](https://i.imgur.com/MiYebzt.png)
* 如果出现如下图错误
	 ![](https://i.imgur.com/qbwv47D.png)
    	* 我的解决办法就是修改数据库密码  在命令行执行命令: mysqladmin -uroot -p原密码 password 新密码
    	* 修改成功后使用新密码登陆数据库
	    	* ![](https://i.imgur.com/lbZH5I8.png)