	access-list [access-list-number] [permit|deny] [ip] [netmask] //创建访问控制列表

	ip nat inside source list [access-list-number] interface [接口号] overload //配置NAT