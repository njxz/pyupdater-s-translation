#1. STEP1   创建密钥包
在一个空的计算机上创建一个密钥包来获得最佳的安全性。你需要输入你的应用的名字。对于同一个应用的密钥包有相同的名字是很重要的。如果你不这么做，你的应用将不能查看更新的数据以及无法自动更新
	
	pyupdater keys -c
#2. 复制密钥包
将密钥包复制到开发环境的电脑上的命令仓库的根目录
#3. 初始化仓库
现在我们需要初始化代码仓库。你需要回答一些关于你的应用的问题，然后directories和config两个文件会被创建。第一个文件夹是pyupdater的工作目录pyu-data，另一个是保存着仓库配置的隐藏文件
	
	pyupdater init
	
#4. 导入密钥对
好了，现在是时候导入我们的密钥包了。确保密钥包文件在代码库的根目录下。在你成功的导入密钥包后，会被安全的删除
	pyupdater keys -i
	
#5. 集成pyupdater
查看  用法|客户端
	
#6. 制作SPEC
你的应用有更多要求的类型么？如果有，你的spec文件必须基于一个pyupdater生成的spec文件。你可以简单的使用下面的代码生成一个。如果你不需要传统的spec文件 跳过下一步。查看spec文件可以在 Danger Zone页下。
	
	pyupdater make-spec -w main.py
	
#7. BUILD
现在让我门来构建我们的应用。在构建时，你有两种选项。你可以指定一个spec文件或者一个主脚本。请查看Danger Zone页来查看版本号
	
	pyupdater build  --app-version=1.0.0 main.spec
	
	pyupdater build --app-version=1.0.0 main.py
	
#8. 创建补丁
是时候创建一个补丁了，如果开启的话，添加一个sha256的散列值到版本列表 并且复制文件到开发文件夹下。你可以结合  --process 和--sign
	
	pyupdater pkg --process
	
#9. 部署密码
现在让我们登录和打包你的版本列表。gzip我们的密钥文件并且同是放置在开发文件夹下。注意，签署进程工作进行时，不需要任何人为介入。你可以结合  --sign和--process
	
	pyupdater pkg --sign
	
#10. 列出已安装的插件
得到一个已经安装的插件列表。你可能需要运行这些多次。
	
	# You can install the official plugins with
	# pip install pyupdater[s3, scp]
	$ pyupdater plugins
	
	s3 by Digital Sapphire
	scp by Digital Sapphire
	
#11. 配置插件
	你的插件也许需要配置，如果你不确定那么请检查这个插件的文档。
	
	pyupdater settings --plugin s3
	
#12. 上传
我们制作好了。是时候上传我们的更新，补丁和更改数据了。第一次上传时，不需要任何的补丁，不需要担心，你可以上传他们在下一次。
	
	pyupdater upload --service s3
	


	
