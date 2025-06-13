#手工配置

	interface port-channel [接口组编号] //创建接口组

	//进入要配置的接口

	channel-group 1 mode on  //划分物理端口到逻辑接口，并指明手工配置

#工业标准

	interface port-channel [接口组号] //创建接口组 

	interface range x/x //进入接口

	channel-protocol lacp 

	channel-group [接口组号] mode active //开启主动模式

#验证配置

	do show etherchannel summary  //查看链路聚合状态
