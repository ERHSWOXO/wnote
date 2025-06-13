[[O.1 配置Enable密码]] //前置条件

	line vty [0] [1~15] //line vty 0 4 表示能同时支持5个并行的虚拟终端

	password [password]

	login

	//前置条件创建本地用户

	login local //使用账号密码登录