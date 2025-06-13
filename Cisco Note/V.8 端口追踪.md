前置
[[V.6 VRRP（虚拟路由器冗余协议）配置]]

	//先在全局模式下配置，再到端口下应用

	track [traack号] interface [接口号] line-protocol 对接口[接口号]状态定义一个track对象[traack号]

	interface [接口号] 

	vrrp [vrrp号] track [track号] decrement [降低多少优先级] //当track绑定的端口出现故障时vrrp的优先级降低30