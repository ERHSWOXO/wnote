#操作系统：Debian12-7 #官方源 #DNS 

# 安装bind9软件包

	root@debian:~#  apt install bind9 -y
# 尝试启动服务并查看状态

	root@debian:~# systemctl start bind9 && systemctl status bind9

![[Pasted image 20241030091430.png]]
# 进入bind的主目录

	root@debian:~# cd  /etc/bind/

# 新建一个域的正向和反向的配置文件

![[Pasted image 20241030093423.png]]

# 从模板创建单个记录文件

![[Pasted image 20241030094310.png]]

# 编辑正向记录文件
新增了一条www的a记录
![[Pasted image 20241030101624.png]]
# 编辑反向记录文件
为刚刚的正向记录创建PTR反向记录
>反向的文件一定要在最后加.
![[Pasted image 20241030111958.png]]
# 使用检查命令

	root@debian:/etc/bind# named-checkconf 
#### 发现错误
![[Pasted image 20241030101902.png]]
解决
![[Pasted image 20241030102745.png]]
不再输出报错
# 客户端验证

正向和反向都正常运行
![[Pasted image 20241030112210.png]]