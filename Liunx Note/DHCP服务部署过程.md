#操作系统：Debian11-7 
## 安装DHCP需要的软件包

```
apt install isc-dhcp-server  -y
```

## 修改dhcp配置文件，以修改分发的网络信息

##### 找到默认的模板并复制黏贴(记得取消最前面的注释符号)
>//定义一个子网 需要填写网段+网段子网掩码
	subnet 10.5.5.0 netmask 255.255.255.224 {                
>//定义地址池 | 定义了一个可分配 ip 地址的范围
	range 10.5.5.26 10.5.5.30;
>//指定域名服务器（DNS）的地址，可为域名可为ip
	option domain-name-servers ns1.internal.example.org;
>//指定域名后缀 一般不用直接注释掉就可以了
	option domain-name "internal.example.org";
>//定义分配的网关地址
	option routers 10.5.5.1;
>//设置dhcp服务使用的广播地址
	option broadcast-address 10.5.5.31;
>//这是默认分配的租约时间
	default-lease-time 600;
>//设置最大可以分配的租约时间
	max-lease-time 7200;
>规范
	#}


## 如果多网卡的情况下，在修改完之后需要指定一下分发的网卡

```
vim /etc/default/isc-dhcp-server 
```
### 在INTERFACESv4里写上网卡（ipv4）

```
INTERFACESv4="ens36"
```

## 然后重启服务查看是否有报错

```
systemctl restart isc-dhcp-server.service 
```

# 配置服务开机自启动

```
systemctl enable isc-dhcp-server.service 
```

---
---
在写教程最后一步的时候发现服务启动失败

> [!NOTE] 报错
> root@debian:~# systemctl restart isc-dhcp-server.service 
Job for isc-dhcp-server.service failed because the control process exited with error code.
See "systemctl status isc-dhcp-server.service" and "journalctl -xe" for details.

输入journalctl -xe去查看详细报错信息

> [!NOTE] 报错
> root@debian:~# journalctl -xe
Aug 13 08:14:20 debian dhcpd[2200]:                              ^
Aug 13 08:14:20 debian isc-dhcp-server[2200]: /etc/dhcp/dhcpd.conf line 111: 350 exceeds max (255) for precision.
Aug 13 08:14:20 debian isc-dhcp-server[2200]:   range 172.16.30.300 172.16.350
Aug 13 08:14:20 debian isc-dhcp-server[2200]:                              ^
Aug 13 08:14:20 debian dhcpd[2200]: /etc/dhcp/dhcpd.conf line 111: too few numbers.
Aug 13 08:14:20 debian dhcpd[2200]:   range 172.16.30.300 172.16.350 ;
Aug 13 08:14:20 debian dhcpd[2200]:                                   ^
Aug 13 08:14:20 debian isc-dhcp-server[2200]: /etc/dhcp/dhcpd.conf line 111: too few numbers.
Aug 13 08:14:20 debian isc-dhcp-server[2200]:   range 172.16.30.300 172.16.350 ;
Aug 13 08:14:20 debian isc-dhcp-server[2200]:                                   ^
Aug 13 08:14:20 debian dhcpd[2200]: Configuration file errors encountered -- exiting
Aug 13 08:14:20 debian isc-dhcp-server[2200]: Configuration file errors encountered -- exiting
Aug 13 08:14:20 debian dhcpd[2200]: 
Aug 13 08:14:20 debian dhcpd[2200]: If you think you have received this message due to a bug rather
Aug 13 08:14:20 debian isc-dhcp-server[2200]: If you think you have received this message due to a bug rather
Aug 13 08:14:20 debian dhcpd[2200]: than a configuration issue please read the section on submitting
Aug 13 08:14:20 debian isc-dhcp-server[2200]: than a configuration issue please read the section on submitting
Aug 13 08:14:20 debian dhcpd[2200]: bugs on either our web page at www.isc.org or in the README file
Aug 13 08:14:20 debian isc-dhcp-server[2200]: bugs on either our web page at www.isc.org or in the README file
Aug 13 08:14:20 debian dhcpd[2200]: before submitting a bug.  These pages explain the proper
Aug 13 08:14:20 debian isc-dhcp-server[2200]: before submitting a bug.  These pages explain the proper
Aug 13 08:14:20 debian dhcpd[2200]: process and the information we find helpful for debugging.
Aug 13 08:14:20 debian isc-dhcp-server[2200]: process and the information we find helpful for debugging.
Aug 13 08:14:20 debian dhcpd[2200]: 
Aug 13 08:14:20 debian dhcpd[2200]: exiting.
Aug 13 08:14:20 debian isc-dhcp-server[2200]: exiting.
Aug 13 08:14:20 debian systemd[1]: isc-dhcp-server.service: Control process exited, code=exited, status=1/FAILURE

发现是我的/etc/dhcp/dhcpd.conf 文件里有写错

> [!NOTE]
> Aug 13 08:14:20 debian isc-dhcp-server[2200]: /etc/dhcp/dhcpd.conf line 111: 350 exceeds max (255) for precision.

排错完毕，修改完配置后服务正常启动
