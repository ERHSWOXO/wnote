
# 安装HTTPD服务

	yum install httpd -y
# 修改配置文件
	[root@server ~]# vim /etc/httpd/conf/httpd.conf

>设置默认目录

![[Pasted image 20241018133922.png]]

>设置目录权限

![[Pasted image 20241018134155.png]]

# 完成修改之后重启服务

	[root@server ~]# systemctl restart httpd

# 查看服务状态
	[root@server ~]# systemctl status httpd

![[Pasted image 20241018135100.png]]