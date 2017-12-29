PyUpdater支持3个发布通道。在向- app-version标志提供版本号时指定发布通道。仅为稳定通道创建补丁。下面的例子，。

##案例---设置通道
	
稳定版：

	$ pyupdater build --app-version=3.30.1
	$ pyupdater build --app-version=2.1
	$ pyupdater build --app-version=1.0


Beta版：

	$ pyupdater build --app-version=1.0.1b
	$ pyupdater build --app-version=3.1b2


Alpha版：
	$ pyupdater build --app-version=1.0.1a
	$ pyupdater build --app-version=5.0alpha	
	$ pyupdater build --app-version=1.1.1alpha1

## 案例---升级检查：
以下的案例是在检查升级时指定通道：

	# Requesting updates from the beta channel
	app_update = client.update_check(APP_NAME, APP_VERSION, channel='beta')
	
	# If no channel is specified, stable will be used
	app_update = client.update_check(APP_NAME, APP_VERSION)


异步下载案例：

	app_update = client.update_check(APP_NAME, APP_VERSION)
	if app_update:
	    app_update.download(async=True)
	
	# To check the status of the download
	# Returns a boolean
	app_update.is_downloaded()


案例：设置一个或多个反馈。Pyupdater 在插件列表上调用 set()，以确保不添加重复的。

	# progress hooks get pass a dict with the below keys.
	# total: total file size
	# downloaded: data received so far
	# status: will show either downloading or finished
	# percent_complete: Percentage of file downloaded so far
	# time: Time left to complete download
	def progress(data):
	    print('Time remaining'.format(data['time']))
	
	def log_progress(data):
	    log.debug('Total file size %s', data['total'])


	# You can initialize the client with a callbacks
	client = Client(ClientConfig(), progress_hooks=[progress, log_progress])
	
	# Or you can add them later.
	client = Client(ClientConfig())
	client.add_progress_hook(log_progress)
	client.add_progress_hook(progress)





