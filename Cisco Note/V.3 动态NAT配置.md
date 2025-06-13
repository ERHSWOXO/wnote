	ip nat pool [pool-number] [起始的ip地址] [结束的ip地址] netmask [地址池ip的子网掩码] // 配置地址池

	access-list [access-list-number] [permit|deny] [ip] [netmask] //创建访问控制列表

	ip nat inside source list [access-list-number] pool [pool-number]  //关联ACL和地址池 

	ip nat inside/outside //确认每个接口的内外网关系