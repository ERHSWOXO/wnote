	interface g0/0 //开启总接口

	no shutdown 

	interface g0/0.xx //进入子接口

	encapsulation dot1Q [VlanID] //配置子接口先封装dota1Q协议