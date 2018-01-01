# 自我更新的Wxpython应用的演示

## 从源运行
[pyupdater-wx-demo](https://github.com/wettenhj/pyupdater-wx-demo)这个仓库提供了一个自我更新的WXpython应用的演示。使用[PyUpdater](http://www.pyupdater.org/),建立在[Pyinstaller](http://www.pyinstaller.org/)之上。

PyUpdater的命令行接口详细描述看这里：[http://www.pyupdater.org/usage-cli/](http://www.pyupdater.org/usage-cli/)

开始尝试运行pyupdater-wx-demo的run.py脚本:

	$ python run.py
	client_config.py is missing.
	You need to run: pyupdater init
	See: http://www.pyupdater.org/usage-cli/
在运行	<font color=#E74C3C>pyupdater init</font>(下面的描述),我们可以引导一个wxpython演示应用：

	$ python run.py

![](http://pyupdater-wx-demo.readthedocs.io/en/latest/_images/run.py_after_PyUpdater_init.png)

为了使得更新可用，我们需要运行<font color=#E74C3C >pyupdater build</font>和<font color=#E74C3C>pyupdater pkg</font>(see [http://www.pyupdater.org/usage-cli/](http://www.pyupdater.org/usage-cli/)),初始化keypack后([http://www.pyupdater.org/commands/#keys](http://www.pyupdater.org/commands/#keys))将会用来签署更新。一旦更新可用，我们需要重新运行一下演示：
	
	$python run.py

如果我们运行了<font color=#E74C3C>python run.py</font>，而不是冻结<font color=#E74C3C>run.exe</font>或<font color=#E74C3C>PyUpdaterWXdemo.exe</font>二进制文件，那么PyUpdater不会再发现新的版本时重启。

# 初始化Pyupdater配置
为了构建和签署演示的  <font color=#E74C3C>冻结（？）</font> 版本（<font color=#E74C3C>PyUpdaterWxDemo.exe </font> 版本 0.0.1 and 0.0.2）

我们会使用<font color=#E74C3C>pyupdater build </font> 和<font color=#E74C3C>pyupdater pkg </font> ,但首先，我们需要为我们的仓库初始化Pyupdater配置和创建一个<font color=#E74C3C>keypack.pyu</font> (为了签署安装包)和导入keypack到我们的Pyupdater配置中去。

	
我们会运行<font color=#E74C3C>pyupdater init</font>从有<font color=#E74C3C>pyupdater-wx-demo/</font> 的仓库文件夹中初始化Pyupdater的配置：

	$ pyupdater init
	Please enter app name
	[DEFAULT] -> PyUpdater App
	Press Enter To Use Default
	--> PyUpdaterWxDemo
	You entered PyUpdaterWxDemo, is this correct?
	[N/y]?y
	Please enter your company or name
	[DEFAULT] -> PyUpdater App
	Press Enter To Use Default
	--> Company Name
	You entered Company Name, is this correct?
	[N/y]?y
	Enter a url to ping for updates. - No Default Available
	--> http://www.example.com
	You entered http://www.example.com, is this correct?
	[N/y]?y
	Would you like to add another url for backup?
	[N/y]?n
	Would you like to enable patch updates?
	[Y/n]?y
	Please enter the path to where pyupdater will write the client\_config.py file. You'll need to import this file to initialize the update process.
	Leave blank to use the current directory
	[DEFAULT] -> pyupdater-wx-demo
	Press Enter To Use Default
	-->
	You entered pyupdater-wx-demo, is this correct?
	[N/y]?y

<font color=#E74C3C>pypdater init</font>命令会创建<font color=#E74C3C>client_config.py</font>和一个<font color=#E74C3C>.pyupdater/config.pyu</font>JSON配置文件，和一个<font color=#E74C3C>pyu-data</font>的文件夹，用来存储包的二进制构筑文件。我们的[FLASK](http://flask.pocoo.org/)文件服务器的URL会基于开放的端口变化，所以现在我们仅输入一个占位URL就可以了（[http://www.example.com](http://www.example.com)）

如果你想要删除再<font color=#E74C3C>.pyupdater/</font>下的数据，你可以运行<font color=#E74C3C>pyupdater clean</font>.

为了创建 <font color=#E74C3C>keypack.pyu</font>:

	$ pyupdater keys -c
	Are you sure you want to continue?
	[N/y]?y
	Please enter app name - No Default Available
	--> PyUpdaterWxDemo
	You entered PyUpdaterWxDemo, is this correct?
	[N/y]?y
	[INFO] Keypack placed in cwd
### 注意：keypack包含了私钥，应该确保是安全的

keypack以JSON格式存储并且使用.pyu后缀（Pyupdater的）

为了引入keypack到你的Pyupdater配置中去：

	Are you sure you want to continue?
	[N/y]?y
	[INFO] Keypack import successfully
	[INFO] Saving Config
	[INFO] Config saved
	[INFO] Wrote client config

你应该在导入后将私钥保存到其他地方，并删除在你的目录下的私钥。

# 建立一个
