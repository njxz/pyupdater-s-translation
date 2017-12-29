#1.导入和常数
client_config.py  默认创建在仓库的根目录
	
	from pyupdater.client import Client
	from client_config import ClientConfig
	
	APP_NAME = 'Super App'
	APP_VERSION = '1.1.0'
	
	ASSET_NAME = 'ffmpeg'
	ASSET_VERSION = '2.3.2'
	
#2.创建反馈
反馈回打印下载进程
	
	def print_status_info(info):
	    total = info.get(u'total')
	    downloaded = info.get(u'downloaded')
	    status = info.get(u'status')
	    print downloaded, total, status
	

#3A.初始化客户端

使用Clientconfig和延迟调用更新来获取最新的更新数据。你也可以添加hooks进程。

	client = Client(ClientConfig())
	client.refresh()
	
	client.add_progress_hook(print_status_info)
	
	
#3B.初始化客户端 alt

使用clientconfig来初始化客户端，添加hook进程和初始化期间刷新。
	client = Client(ClientConfig(), refresh=True,
	                        progress_hooks=[print_status_info])
	
#4A 更新检查

更新检查检查到可更新时，返回一个LibUpdate对象
	
	lib_update = client.update_check(APP_NAME, ASSET_VERSION)

#4B 更新检查alt

在beta通道上检查更新

	lib_update = client.update_check(ASSET_NAME, ASSET_VERSION, channel='beta')
#5A  下载更新
如果我们获得一个更新对象，我们可以继续下载更新
	if lib_update is not None:
	    lib_update.download()
	
#5B 下载更新alt
	
我们也能下载一个后台进程


	if lib_update is not None:
	    lib_update.download(async=True
	
#6A 覆盖
确保文件下载成功后，解压更新和覆盖当前的应用
	
	if lib_update.is_downloaded():
	    lib_update.extract()
	
	# Update will be extracted in the update folder
	lib_update.update_folder

