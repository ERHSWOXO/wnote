	ospf [ospf-id]

	route-id [route-id]

	network [要通告的网段] [反mask] area [area-id]

	no auto-summary//禁止自动汇总

	redistribute [路由协议] [路由进程号] subnets metric-type [类型1/类型2] /路由引入

	default-information originate  //下放默认路由

刷新路由表



>进入接口
	ip ospf network point-to-point    //修改OSPF类型为点对点

	area [area-id] virtual-link [route-id] //虚拟链路配置
	redistribute ospf [ospf-id] //在配置vlink后路由引入ospf

	interface e0/1 //进入与邻居相连的口子
	ip ospf priority 0  //优先级是0的时候说明改设备不适合做DR/BDR