* #python-django安装
	* ###建立虚拟环境 
	
		* ####创建一个文件夹 命令行进入该文件夹
		
		* ####如果你使用的是python3 使用命令 python -m venv llenv
		
		* ####如果以上命令执行成功就不需要看安装virtualenv
	* ###安装virtualenv
		* ####执行该命令 pip install --user virtualenv
		
		* ####注意：使用的是linux系统，并且上面的命令不起作用，可使用系统的包管理器来安装virtualenv
		
		* ####如果是ubuntu系统可以使用 sudo apt-get install python-virtualenv
	* ###激活虚拟环境
		* ####linux系统使用命令 source ll_env/bin/activate
		
		* ####windows系统使用 ll_env\Scripts\activate
	* ###停止虚拟环境
		* <h4>使用命令 deactivate</h4>
	
	* ###安装Django
	
		* <h4>使用命令 pip install Django</h4>
		
	* ###在Django中创建项目
		* ####使用命令 django-andmin startproject 项目名称
		
		* ####执行上条命令成功后会生成对应的项目文件夹，生成系统文件 settings.py urls.py wsgi.py 
	* ###创建数据库
		* ####执行命令 python manage.py makemigrations 生成新的迁移文件
		
		* ####执行命令 python manage.py migrate     执行新的迁移文件
	* ###运行项目
		* ####执行命令 python manage.py runserver
		
		* ####指定运行端口命令为 python manage.py runserver 端口号
	* ###创建应用程序
		* ####在虚拟环境激活的情况下执行 python manage.py startapp 应用名称
		
		* ####执行上条命令会在应用名称文件夹下面创建多个文件，最重要的文件就是，models.py admin.py views.py 
	* ###定义模型
		* <h4>一个模型就是一张数据库表</h4>
	* ###激活模型
		* ####在setting.py文件中的INSTALLED_APPS片段中加入自己的应用程序名称
		
		* ####执行命令 python manage.py makemigrations 应用名称
		 