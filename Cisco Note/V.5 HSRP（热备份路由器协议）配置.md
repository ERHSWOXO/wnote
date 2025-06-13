
	standby [standby_id] ip [虚拟网关的ip]   //启用HSRP，并设置虚拟网关的IP地址，1为standby组号

	//相同组号的路由器属于同一个HSRP组，所有属于同一个HSRP组的路由器的虚拟IP地直址必须一致

	standby 1 priority 120 //设置HSRP的优先级，若不设置，默认是100，该值越大，抢占为活动路由器的优先权越高

	standby 1 preempt  //设置路由器在最高优先级时成为活动路由器

R1(config-if)#standby 1 timers 3 10

//其中3s为hello time，表示路由器多长时间发送hello消息

      10s为hold time，表示在10秒内同组内的其他路由器没有收到活动路由器的消息，则认为活动路由器出现故障了。

R1(config-if)#standby 1 authentication md5 key-string cisco

//配置认证密码，防止非法设备加入 HSRP组中，同一个组的密码一致




R3(config)#interface e0/1

R3(config-if)#standby 1 ip 192.168.13.254

R3(config-if)#standby 1 preempt

R3(config-if)#standby 1 timers 3 10

R3(config-if)#standby 1 authentication md5 key-string cisco