	• PyUpdater通过setuptools的entry points来寻找插件
	• 基础类提供了hepler方法来获得和设置 配置信息

##简单的案例：

my_uploader.py


	from pyupdater.uploader import BaseUploader
	
	
	class MyUploader(BaseUploader):
	
	    name = 'my uploader'
	    author = 'Jane Doe'
	
	    def init_config(self, config):
	        self.server_url = config["server_url"]
	
	    def set_config(self, config):
	        server_name = self.get_answer("Please enter server name\n--> ")
	        config["server_url"] = server_name
	
	    def upload_file(self, filename):
	        # Make the magic happen
	        files = {'file': open(filename, 'rb')}
	        r = request.post(self.server_url, files=files)


在你的setup.py

	setup(
	    provides=['pyupdater.plugins',],
	    entry_points={
	        'pyupdater.plugins': [
	            'my_uploader = my_uploader:MyUploader',
	            ]
	        },


##插件设置

插件作者有两种方式去获得和设置配置信息

第一种方法会从用户处获得信息。在你的插件中你需要做一下像下面的事情:

	# Saves the config to disk.
	def set_config(self, config):
	    server_name = self.get_answer("Please enter server name\n--> ")
	    config["server_url"] = server_name
	
	
	# Will be called after the class is initialized.
	def init_config(self, config):
	    self.server_url = config["server_url"]


插件案例：

[S3 插件](https://github.com/JMSwag/PyUpdater-S3-Plugin)

[SCP 插件](https://github.com/JMSwag/PyUpdater-SCP-Plugin)
