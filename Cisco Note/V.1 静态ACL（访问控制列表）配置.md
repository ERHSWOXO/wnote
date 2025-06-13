	标准ACL语句
	access-list [access-list-number] [permit|deny] [host|source source-wildcard|any] //[tcp/icmp/ip]
	
	启用ACL
	//前置条件：进入接口
	ip access-group [access-list-number] [in|out] //调用ALC的方向








































<待学习>

	基于时间的ACL
	time-range [时间范围名字]




ACL配置：

  1. 创建ACL列表：
   access-list  <num> deny | permit  tcp/icmp/ip .....

  2、接口下应用acl规则
    ip access-group acl-num in | out

  access-list和 ip access-lit的区别：
  access-list只能接数字，ip accesss-list可以接规则名称，方便记忆，扩展性更好


ACL匹配的信息：
   五元组（源IP地址，目的IP地址，协议号，目的端口，源端口）、源MAC地址、目的MAC地址、VLAN、DSCP值等等

其他参数：
   time-rang <time>0/1
      periodic + 周期



