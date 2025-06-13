#系统环境：Centos7 

# 检查环境是否支持

	 cat /proc/cpuinfo | grep vmx

# 安装KVM需要的软件包

	yum install qemu* libvirt virt* bridge-utils -y

# 安装虚拟化套件

#### 检索所有套件
	[root@server-1 ~]# yum grouplist
	Loaded plugins: fastestmirror
	There is no installed groups file.
	Maybe run: yum groups mark convert (see man yum)
	Loading mirror speeds from cached hostfile
	Available Environment Groups:
	   Minimal Install
	   Compute Node
	   Infrastructure Server
	   File and Print Server
	   Basic Web Server
	   Virtualization Host
	   Server with GUI
	   GNOME Desktop
	   KDE Plasma Workspaces
	   Development and Creative Workstation
	Available Groups:
	   Compatibility Libraries
	   Console Internet Tools
	   Development Tools
	   Graphical Administration Tools
	   Legacy UNIX Compatibility
	   Scientific Support
	   Security Tools
	   Smart Card Support
	   System Administration Tools
	   System Management
	Done
#### 安装Virtualization Host套件

	[root@server-2 ~]# yum groupinstall " Virtualization Host"
# 启动组件设置开机自启动

	[root@server-2 ~]# systemctl restart libvirtd
	[root@server-2 ~]# systemctl enable libvirtd

# 创建磁盘映像文件
	[root@localhost ~]# qemu-img create -f qcow2 /mnt/vm/centos1511.qcow2 40G

![[Pasted image 20241025133434.png]]
# 查看磁盘映像文件



# 开始启动虚拟机
>[root@localhost ~]# virt-install --name centos \
> --vrit-type kvm \
> --ram 4096 
> --vpus 2\
> --cdrom /mnt/vm/1511.iso \
> --disk path=/mnt/vm/centos1511.qcow2 
>  --disk path=/dev/vmdisk/r9disk \                       //使用物理磁盘
> --network network=default \
> --graphics vnc, listen=0.0.0.0 \
> --noautoconsole

### 出现这个代表启动成功
Starting install...
Creating domain...                                       |    0 B     00:00     
Domain installation still in progress. You can reconnect to 
the console to complete the installation process.

# 检查虚拟器状态

	[root@localhost ~]# virsh list --all

![[Pasted image 20241025140611.png]]

# 启动虚拟机

	[root@localhost ~]# virsh start centos
	Domain centos started

![[Pasted image 20241025140935.png]]

# 关闭虚拟机

	[root@localhost ~]# virsh shutdown centos
	Domain centos is being shutdown

![[Pasted image 20241025141114.png]]

# 使用VNC链接图形化管理虚拟机
地址是刚刚写的侦听地址

![[Pasted image 20241025140711.png]]


