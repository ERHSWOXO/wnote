# 创建PV单元

	[root@localhost ~]# pvcreate /dev/sdb

![[Pasted image 20241025132715.png]]
![[Pasted image 20241025132758.png]]

# 创建VG卷组

	[root@localhost ~]# vgcreate Vstorage /dev/sdb

![[Pasted image 20241025132913.png]]
![[Pasted image 20241025132933.png]]

# 创建LV逻辑卷

	lvcreate -n VHOST -l 100%FREE Vstorage

![[Pasted image 20241025133050.png]]
![[Pasted image 20241025133109.png]]

# 格式化逻辑卷

	[root@localhost ~]# mkfs.xfs /dev/mapper/Vstorage-VHOST 

![[Pasted image 20241025133535.png]]

# 挂载使用

	[root@localhost ~]# mount /dev/mapper/Vstorage-VHOST /mnt/vm/
