在成功挂载系统上后

记住一定要换个位置推荐/tmp

	cp /mnt/cdrom/VMwareTools-x.x.x-yyyy.tar.gz /tmp

解压VMwareTools的包

	tar zxpf /mnt/cdrom/VMwareTools-x.x.x-yyyy.tar.gz

然后进入解压的目录执行安装脚本就好

	cd vmware-tools-distrib 
	sudo ./vmware-install.pl