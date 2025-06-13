#系统环境：Centos7 

![[Pasted image 20241018135353.png]]
![[Pasted image 20241018135453.png]]
# 安装NFS所需软件包

	[root@server ~]# yum install nfs-utils rpcbind -y

# 启动两个服务

	[root@server ~]# systemctl restart nfs-utils && systemctl status nfs-utils && systemctl enable nfs-utils

![[Pasted image 20241018135857.png]]

	[root@server ~]# systemctl restart rpcbind && systemctl status rpcbind && systemctl enable rpcbind

![[Pasted image 20241018135913.png]]

# 启动NFS服务

	[root@server ~]# systemctl restart nfs && systemctl status nfs

![[Pasted image 20241018141822.png]]
# 编辑NFS服务配置文件

![[Pasted image 20241018140424.png]]
写入目录   nfs服务器ip （权限）
![[Pasted image 20241018141230.png]]

# 编辑完之后如写入

	exportfs -r 
# 客户端也安装两个软件包

