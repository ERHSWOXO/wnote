# 1.   职业素养

1.整理赛位，工具、设备归位，保持赛后整洁有序。

2.无因选手原因导致设备损坏。

3.恢复调试现场，保证网络和系统安全运行。

# 2.   网络连接

1．根据“图1”的要求，截取适当长度和数量的双绞线，端接水晶头，制作网络线缆，根据 “表1”和 “表2”进行设备之间端口的互连，设备接口地址的配置。

# 3.   交换配置

1.配置vlan，SW1、SW2、SW3、AC1的二层链路只允许相应vlan通过。

	SW1(config)#vlan 10;20;30;40;50;60;70;80;90
	SW2(config)#vlan 10;20;30;40;50;60;70;80;90
	SW3(config)#vlan 10;20;30;50;60;70;80;90

	  int e1/0/1;2;3;4;5;6;7;8;9
	  switchport mode access
	  exit
	  int e1/0/1
	  switchport access vlan 10
	  exit
	  int e1/0/2
	  switchport access vlan 20
	  exit
	  int e1/0/3
	  switchport access vlan 30
	  exit
	  int e1/0/4
	  switchport access vlan 40
	  exit
	  int e1/0/5
	  switchport access vlan 50
	  exit
	  int e1/0/6
	  switchport access vlan 60
	  exit
	  int e1/0/7
	  switchport access vlan 70
	  exit
	  int e1/0/8
	  switchport access vlan 80
	  exit
	  int e1/0/9
	  switchport access vlan 90
	  exit
SW3
	  int e1/0/1;2;3;5;6;7;8;9
	  switchport mode access
	  exit
	  int e1/0/1
	  switchport access vlan 10
	  exit
	  int e1/0/2
	  switchport access vlan 20
	  exit
	  int e1/0/3
	  switchport access vlan 30
	  exit
	  int e1/0/5
	  switchport access vlan 50
	  exit
	  int e1/0/6
	  switchport access vlan 60
	  exit
	  int e1/0/7
	  switchport access vlan 70
	  exit
	  int e1/0/8
	  switchport access vlan 80
	  exit
	  int e1/0/9
	  switchport access vlan 90
	  exit

2.SW1、SW2、SW3启用MSTP，实现网络二层负载均衡和冗余备份，创建实例Instance10和Instance20，名称为SKILLS，修订版本为1，其中Instance10关联vlan60和vlan70，Instance20关联vlan80和vlan90。SW1为Instance0和Instance10的根交换机，为Instance20备份根交换机；SW2为Instance20根交换机，为Instance0和Instance10的备份根交换机；根交换机STP优先级为0，备份根交换机STP优先级为4096。关闭交换机之间三层互联接口的STP。

	spanning-tree
	spanning-tree mst configuration
	name SKILLS
	revision-level 1
	instance 0 vlan 1-59;61-69;71-79;81-89;91-4094
	instance 10 vlan 60;70
	instance 20 vlan 80;90
	exit

SW1(config)#spanning-tree mst 0 priority 0 
SW1(config)# spanning-tree mst 10 priority 0  
SW1(config)# spanning-tree mst 20 priority 4096

SW2(config)#spanning-tree mst 0 priority 4096
SW2(config)#spanning-tree mst 10 priority 4096
SW2(config)#spanning-tree mst 20 priority 0 

	spanning-tree mode mstp

SW1(config)#int e1/0/21;22;26;27
SW1(config-if-port-range)#no spanning-tree 
SW1(config-if-port-range)#exit

SW2(config)#int e1/0/11;12;13;14;21;22;26;27
SW2(config-if-port-range)#no spanning-tree
SW2(config-if-port-range)#exit

SW3(config)#int e1/0/21;22;15;17;18
SW3(config-if-port-range)#no spanning-tree 
SW3(config-if-port-range)#exit


3.SW1和SW2之间利用三条裸光缆实现互通，其中一条裸光缆承载三层IP业务、一条裸光缆承载VPN业务、一条裸光缆承载二层业务。用相关技术分别实现财务1段、财务2段业务路由表与其它业务路由表隔离，财务业务VPN实例名称为CW。承载二层业务的只有一条裸光缆通道，配置相关技术，方便后续链路扩容与冗余备份，编号为1，用LACP协议，SW1为active，SW2为active；采用源、目的IP进行实现流量负载分担。

SW1(config)#vlan 1027
SW1(config-vlan1027)#exit
SW1(config)#
SW1(config)#ip vrf CW
SW1(config-vrf)#exit 
SW1(config)#int vlan 40
SW1(config-if-vlan40)#ip vrf forwarding CW
SW1(config-if-vlan40)#exit
SW1(config)#int vlan 1027
SW1(config-if-vlan1027)#ip vrf forwarding CW
SW1(config-if-vlan1027)#exit

SW2(config)#vlan 1027
SW2(config-vlan1027)#exit
SW2(config)#
SW2(config)#ip vrf CW
SW2(config-vrf)#exit 
SW2(config)#int vlan 40
SW2(config-if-vlan40)#ip vrf forwarding CW
SW2(config-if-vlan40)#exit
SW2(config)#int vlan 1027
SW2(config-if-vlan1027)#ip vrf forwarding CW
SW2(config-if-vlan1027)#exit


SW2(config)#port-group 1
SW2(config)#interface e1/0/28
SW2(config-if-ethernet1/0/28)#port-group 1 mode active 
SW2(config-if-ethernet1/0/28)#exit
SW2(config)#load-balance dst-src-ip 

4.将SW3模拟为Internet交换机，实现与集团其它业务路由表隔离，Internet路由表VPN实例名称为Internet。将SW3模拟办事处交换机，实现与集团其它业务路由表隔离，办事处路由表VPN实例名称为Guangdong。

ip vrf Guangdong

ip vrf Internet

按照题目接口表配置所有IPV4 V6 地址，保证直连互通


5.SW1法务物理接口限制收发数据占用的带宽均为1500Mbps，限制所有报文最大收包速率为2000packets/s，如果超过了配置交换机端口的报文最大收包速率则关闭此端口，1分钟后恢复此端口；启用端口安全功能，最大安全MAC地址数为20，当超过设定MAC地址数量的最大值，不学习新的MAC、丢弃数据包、发 snmp trap、同时在syslog日志中记录，端口的老化定时器到期后，在老化周期中没有流量的部分表项老化，有流量的部分依旧保留，恢复时间为10分钟；禁止采用访问控制列表，只允许IP主机位为20-50的数据包进行转发；禁止配置访问控制列表，实现端口间二层流量无法互通，组名称FW。


Interface Ethernet1/0/3
 bandwidth control 102400 both
 rate-violation all 100
 rate-violation control shutdown recovery 60
 switchport access vlan 30
 switchport port-security
 switchport port-security maximum 20
 switchport port-security mac-address sticky
 switchport port-security violation restrict
 switchport port-security aging time 10
 switchport port-security aging type inactivity
 am port
 am ip-pool 10.10.13.20 30


6.SW1配置SNMP，引擎id分别为1；创建组GROUP2024，采用最高安全级别，配置组的读、写视图分别为：SKILLS_Ro、SKILLS_Rw；创建认证用户为USER2024，采用aes算法进行加密，密钥为pASS.2024，哈希算法为sha，密钥为pASS.2024；当设备有异常时，需要用本地的环回地址loopback1发送v3Trap消息至集团网管服务器10.10.11.99、2001:10:10:11::99，采用最高安全级别；当法务部门对应的用户接口发生UPDOWN事件时，禁止发送trap消息至上述集团网管服务器。

snmp-server enable
snmp-server securityip 10.10.11.99
snmp-server securityip 2001:10:10:11::99
snmp-server trap-source 10.10.1.2
snmp-server trap-source 2001:10:10:1::2
snmp-server engineid 1
snmp-server group GROUP2024 authpriv read SKILLS_Ro write SKILLS_Rw
snmp-server host 2001:10:10:11::99 v3 authpriv USER2024
snmp-server host 10.10.11.99 v3 authpriv USER2024
snmp-server enable traps
!

# 4.   路由配置

1.配置所有设备接口ipv4地址和ipv6地址，互联接口ipv6地址用本地链路地址。

2.利用vrrpv2和vrrpv3技术实现vlan60、vlan70、vlan80、vlan90网关冗余备份，vrrpid与vlanid相同。vrrpv2vip为10.10.vlanid.9（如vlan60的vrrpv2vip为10.10.60.9），vrrpv3vip为FE80:vlanid::9（如vlan60的vrrpv3vip为FE80:60::9）。配置SW1为vlan60、vlan70的Master，SW2为vlan80、vlan90的Master。要求vrrp组中高优先级为120，低优先级为默认值，抢占模式为默认值，vrrpv2和vrrpv3发送通告报文时间间隔为默认值。当SW1或SW2上联链路发生故障，Master优先级降低50。

3.SW1、SW2、SW3、RT1以太链路、RT2以太链路、FW1、FW2、AC1之间运行OSPFv2和OSPFv3协议（路由模式发布网络用接口地址，BGP协议除外）。

(1)SW1、SW2、SW3、RT1、RT2、FW1之间OSPFv2和OSPFv3协议，进程1，区域0，分别发布loopback1地址路由和产品路由，FW1通告type2默认路由。

(2)RT2与AC1之间运行OSPFv2协议，进程1，nssa no-summary区域1；AC1发布loopback1地址路由、产品和营销路由，用prefix-list重发布loopback3。

(3)RT2与AC1之间运行OSPFv3协议，进程1，stub no-summary区域1；AC1发布loopback1地址路由、产品和营销。

(4)SW3模拟办事处产品和营销接口配置为loopback，模拟接口up。SW3模拟办事处与FW2之间运行OSPFv2协议，进程2，区域2，SW3模拟办事处发布loopback2、产品和营销。SW3模拟办事处配置ipv6默认路由；FW2分别配置到SW3模拟办事处loopback2、产品和营销的ipv6明细静态路由，FW2重发布静态路由到OSPFv3协议。

(5)RT1、FW2之间OSPFv2和OSPFv3协议，进程2，区域2；RT1发布loopback4路由，向该区域通告type1默认路由；FW2发布loopback1路由，FW2禁止学习到集团和分公司的所有路由。RT1用prefix-list匹配FW2 loopback1路由、SW3模拟办事处loopback2和产品路由、RT1与FW2直连ipv4路由，将这些路由重发布到区域0。

(6)修改ospf cost为100，实现SW1分别与RT2、FW2之间ipv4和ipv6互访流量优先通过SW1_SW2_RT1链路转发，SW2访问Internet ipv4和ipv6流量优先通过SW2_SW1_FW1链路转发。

4.RT1串行链路、RT2串行链路、FW1、AC1之间分别运行RIP和RIPng协议，FW1、RT1、RT2的RIP和RIPng发布loopback2地址路由，AC1RIP发布loopback2地址路由，AC1RIPng采用route-map匹配prefix-list重发布loopback2地址路由。RT1配置offset值为4的路由策略，实现RT1-S1/0_RT2-S1/1为主链路，RT1-S1/1_RT2-S1/0为备份链路，ipv4的ACL名称为AclRIP，ipv6的ACL名称为AclRIPng。RT1的S1/0与RT2的S1/1之间采用chap双向认证，用户名为对端设备名称，密码为pASS.2024。

5.RT1以太链路、RT2以太链路之间运行ISIS协议，进程1，分别实现loopback3之间ipv4互通和ipv6互通。RT1、RT2的NET分别为10.0000.0000.0001.00、10.0000.0000.0002.00，路由器类型是Level-2，接口网络类型为点到点。配置域md5认证和接口md5认证，密码均为pASS.2024。

6.RT2配置ipv4nat，实现AC1ipv4产品部门用RT2外网接口ipv4地址访问Internet。RT2配置nat64，实现AC1ipv6产品部门用RT2外网接口ipv4地址访问Internet，ipv4地址转ipv6地址前缀为64:ff9b::/96。

7.SW1、SW2、SW3、RT1、RT2之间运行BGP协议，SW1、SW2、RT1的AS号65001、RT2的AS号65002、SW3的AS号65003。

(1)SW1、SW2、SW3、RT1、RT2之间通过loopback1建立ipv4和ipv6 BGP邻居。SW1和SW2之间财务通过loopback2建立ipv4 BGP邻居，SW1和SW2的loopback2互通采用静态路由。

(2)SW1、SW2、SW3、RT2分别只发布营销、法务、财务、人力等ipv4和ipv6路由；RT1发布办事处营销ipv4和ipv6路由到BGP。

(3)SW3营销分别与SW1和SW2营销ipv4和ipv6互访优先在SW3_SW1链路转发；SW3法务及人力分别与SW1和SW2法务及人力ipv4和ipv6互访优先在SW3_SW2链路转发，主备链路相互备份；用prefix-list、route-map和BGP路径属性进行选路，新增AS65000。

8.利用BGP MPLS VPN技术，RT1与RT2以太链路间运行多协议标签交换、标签分发协议。RT1与RT2间创建财务VPN实例，名称为CW，RT1的RD值为1:1，export rt值为1:2，import rt值为2:1；RT2的RD值为2:2。通过两端loopback1建立VPN邻居，分别实现两端loopback5的ipv4互通和ipv6互通。

# 5.   无线配置

1.AC1 loopback1 ipv4和ipv6地址分别作为AC1的ipv4和ipv6管理地址。AP二层自动注册，AP采用MAC地址认证。配置2个ssid，分别为SKILLS-2.4G和SKILLS-5G。SKILLS-2.4G对应vlan110，用network110和radio1（模式为n-only-g）,用户接入无线网络时需要采用基于WPA-personal加密方式，密码为pASS.2024。SKILLS-5G对应vlan120，用network120和radio2（模式为n-only-a），不需要认证，隐藏ssid，SKILLS-5G用倒数第一个可用VAP发送5G信号。

2.AC1配置DHCPv4和DHCPv6，分别为SW1产品1段vlan10和分公司vlan100、vlan110和vlan120分配地址；ipv4地址池名称分别为POOLv4-10、POOLv4-100、POOLv4-110、POOLv4-120，ipv6地址池名称分别为POOLv6-10、POOLv6-100、POOLv6-110、POOLv6-120；ipv6地址池用网络前缀表示；排除网关；DNS分别为114.114.114.114和2400:3200::1；为PC1保留地址10.10.11.9和2001:10:10:11::9，为AP1保留地址10.17.100.9和2001:10:17:100::9，为PC2保留地址10.17.110.9和2001:10:17:110::9。SW1上中继地址为AC1 loopback1地址。SW1启用DHCPv4和DHCPv6 snooping，如果E1/0/1连接DHCPv4服务器，则关闭该端口，恢复时间为1分钟。

3.当AP上线，如果AC中储存的Image版本和AP的Image版本号不同时，会触发AP自动升级。AP失败状态超时时间及探测到的客户端状态超时时间都为2小时。

4.MAC认证模式为黑名单，MAC地址为80-45-DD-77-CC-48的无线终端采用全局配置MAC认证。

5.配置vlan110无线接入用户上班时间（工作日09:00-17:00）访问Internet https上下行CIR为100Mbps，CBS为200Mbps，PBS为300Mbps，exceed-action 和violate-action均为drop。时间范围名称、控制列表名称、分类名称、策略名称均为SKILLS。

6.开启AP组播广播突发限制功能；AP收到错误帧时，将不再发送ACK帧； AP发送向无线终端表明AP存在的帧时间间隔为1秒。AP发射功率为80%。

# 6.   安全配置

**【说明：ip地址按照题目给定的顺序用“ip/mask”表示，ipv4 any地址用0.0.0.0/0，ipv6 any地址用::/0，禁止用地址条目，否则按零分处理。】**

1.FW1配置ipv4nat，实现集团产品1段ipv4访问Internet ipv4，转换ip/mask为200.200.200.160/28，保证每一个源ip产生的所有会话将被映射到同一个固定的IP地址；当有流量匹配本地址转换规则时产生日志信息，将匹配的日志发送至10.10.11.99的UDP514端口，记录主机名，用明文轮询方式分发日志；开启相关特性，实现扩展nat转换后的网络地址端口资源。

2.FW1配置nat64，实现集团产品1段ipv6访问Internet ipv4，转换为出接口IP，ipv4转ipv6地址前缀为64:ff9b::/96。

3.FW1和FW2策略默认动作为拒绝，FW1允许集团产品1段ipv4和ipv6访问Internet任意服务。

4.FW2允许办事处产品ipv4访问集团产品1段https服务，允许集团产品 1段和分公司产品访问办事处产品ipv4、FW2 loopback1的ipv4、SW3模拟办事处 loopback2的ipv4。

5.FW1与RT2之间用Internet互联地址建立GRE Over IPSec VPN，实现 loopback4之间的加密访问。

6.FW1配置SSLVPN，名称为VPNSSL，ssl协议为1.2版本，Internet用户通过端口8888连接，本地认证账号UserSSL,密码pASS.2024，地址池名称为POOLSSL，地址池范围为10.18.0.100/24-10.18.0.199/24。保持PC1位置不变，用PC1测试。