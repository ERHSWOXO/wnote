[HUB汇总端]
进入隧道口

	tunnel mode gre multipoint //配置动态多点GRE
	tunnel source [公网地址]   //配置出口
	tunnel key [密钥]          //配置隧道密钥
	ip nhrp network-id [network-id] //配置network-id 
	ip nhrp authentication wsc2024  //配置认证密钥
	ip nhrp map multicast dynamic   //启动多点映射

[Spoke分布端]
进入隧道口

	tunnel mode gre multipoint       //配置动态多点GRE
	tunnel source [公网地址]      //配置出口
	tunnel key [密钥]      //配置隧道
	ip nhrp network-id [network-id] //配置network-id 
	ip nhrp authentication wsc2024  //配置认证密钥
	ip nhrp map [HUB的隧道地址] [HUB的公网地址]       //绑定HUB的公网地址和隧道地址
	ip nhrp map multicast [HUB的公网地址]         //向HUB的公网地址发组播包
	ip nhrp nhs [HUB的隧道地址]       //通告HUB的地址
