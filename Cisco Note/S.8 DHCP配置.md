	service dhcp //启用DHCP

	ip dhcp pool +名字 //添加DHCP地址池

	network xxx.xxx.xxx.xxx /xx 配置地址池网段

	default-router [网关IP] //配置网关
	
接口ip地址
inter gx/x
ip addres xxx.xxx.xxx.xxx +网关
lease x                                                    //租借天数
dns-server ip-addres xxx.xxx.xxx.xxx

	ip dhcp excluded-addres xxx.xxx.xxx.xxx xxx.xxx.xxx.xxx   //排除地址
	//排除范围 如192.168.1.1~192.168.1.10，则DHCP从192.168.1.11开始分配