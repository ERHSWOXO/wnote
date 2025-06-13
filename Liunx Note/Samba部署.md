#系统环境：Centos7 

# 安装Samba服务

	yum install samba samba-common samba-client -y
	
![[Pasted image 20241014105613.png]]
# 关闭服务器Selinux和防火墙

	[root@server ~]# setenforce 0
	[root@server ~]# getenforce 0
	Permissive
	[root@server ~]# systemctl stop firewalld && systemctl status firewalld
# 关闭客户端的

	[root@client ~]# setenforce 0
	[root@client ~]# getenforce 0
	Permissive
	[root@client ~]# systemctl stop firewalld && systemctl status firewalld 
# 创建根目录

	mkdir /var/public

# 复制测试文件

	[root@server public]# cp  /tmp/*.repo .、
# 修改配置文件
	[root@server ~]# vim /etc/samba/smb.conf 
配置工作组
![[Pasted image 20241014111021.png]]
配置机器名称
![[Pasted image 20241014110947.png]]
配置允许访问网段
![[Pasted image 20241014110643.png]]
配置匿名安全策略
![[Pasted image 20241014111059.png]]
创建一个共享
![[Pasted image 20241014111224.png]]

# 启动并验证服务配置

	systemctl restart smb && systemctl status smb 

![[Pasted image 20241014112924.png]]
# 在客户端

# 安装测试工具



# 测试后可以看到共享文件
![[Pasted image 20241014113041.png]]