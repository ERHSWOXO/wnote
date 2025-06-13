>eBGP

	router bgp [BGP-ID]
	 bgp router-id [IP]
	 timers bgp [keeplive ]
	 neighbor [邻居的IP地址] remote-as [邻居的AS号]
其他命令

	route-map active permit 10  //配置优先级
	-route-map)#set local-preference [优先级]  //配置本地优先级
	-router)#neighbor 192.0.2.201 route-map active out  //配置流量out

   
route-map as-path permit 10
set as-path prepend 4259840003 4259840003

>iBGP

前置条件 使用路由协议 neighbor 可以互联

bgp router-id 10.10.0.1
neighbor 10.10.0.1 remote-as 4259840003
neighbor 10.10.0.1 password wsc2024@SH
neighbor 10.10.0.1 update-source Loopback1
