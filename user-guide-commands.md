#命令：#

### 注意：所有的命令必须以root或者管理员运行 ###

#1.Archive

	usage: pyupdater archive [opts] filename 
	
	optional arguments: 
	-h, --help  	显示帮助文档和退出 
	--name NAME 	 Name用来在存档前重命名
	--version VERSION 	 文档的版本
	-k, --keep	存档后，不删除源文件
	
描述：

archive 命令回保存一个你的应用使用的额外的文件，这将会允许他上传这个文件。

例：

如果你的应用依赖于ffmpeg，但是你不想将ffmpeg绑定在你的app里。
更多可以查看  

	"Usage | CLI | Assets" & "Usage | Client | Assets" 
	
例子：

	pyupdater archiver --name ffmpeg --version 2.1.4
	pyupdater archiver --name ffmpeg  --version 2.2
	
	
# 2.Build：
	
	usage: pyupdater build [opts] [app.py|app.spec] optional arguments: 
	-h, --help	 show this help message and exit 
	--clean 	清除build,绕过缓存
	--app-version	 APP_VERSION 
	-k, --keep 	Will not delete executable after archiving
	
	
## 描述:

	build命令将会封装pyinstaller来创建最终的应用程序。所有的选项都通过pyinstaller.一旦构建了可执行文件就归档成了一个pyupdater兼容的格式，而且放置在 pyu-data/new directory.如果你在版本号内有一个alpha或者beta标记，当处理此二进制文件时，将会放置在各自的通道内。需要注意的是，补丁只能在稳定版本上面创建
	
##案例：
**从python脚本上构建**

		pyupdater build -F --app-version 1.0  app.py
	

**从spec文件中创建（在how to create spec files 上查看制作spec文件）**

		pyupdater build --app-version 1.2 app.spec
	
**beta通道**

		pyupdater build --app-version 1.2beta2
	
# 3.Clean:

	usage: pyupdater clean [-h] [-y]
	
	optional arguments:
	  -h, --help	  show this help message and exit
	  -y, --yes  	 确认删除pyu-data & .pyupdater folder
	
##描述：
从当前的仓库中删除所有Pyupdater的痕迹
	
**案例**

	pyupdater clean
	
# 4.Collect Debug info
	sage: pyupdater collect-debug-info [-h]
	
	optional arguments:
	  -h, --help 	 show this help message and exit
	
**描述：**

	上传debug的日志，从pyupdater's的CLI到一个私人要点
	
**案例：**

	pyupdater collect-debug-info
	
#5.Init
	usage: pyupdater init [-h]
	
	optional arguments:
	  -h, --help            show this help message and exit
	
**描述：**

使用pyupdater出事话一个仓库，你需要回答一些关于你的应用的问题。一旦完成了，config目录，data目录和client_config.py配置文件将会被创建。他会在需要的时候安全的删除pyu-data目录。当你上传的时候，一个新的client_config.py文件会被创建。
	
案例：
	
	pyupdaterr init 
	
#6. Keys
	usage: pyupdater keys [-h] [-i] [-c] [-y]
	
	optional arguments:
	  -h, --help   	 show this help message and exit
	  -i, --import  	从当前工作目录导入一个密钥包
	  -c, --create 	 创建一个仅可用于你的离线设备的密钥包
	  -y, --yes    	在你运行时无需手动确认
	
#7.Make Spec
	
#8. Pkg

#9. Plugins

#10. Settings
#11. Upload

#12. Help


	





	1. 
