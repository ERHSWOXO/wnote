#系统环境：Centos7 
# 创建挂载点

	mkdir /mnt/cdrom/
# 把默认的repo文件移至/tmp

	mv /etc/yum.repos.d/* /tmp
# 创建本地repo文件

	vi /etc/yum.repo.d/centos/repo
# 编辑
![[Pasted image 20241014102859.png]]

# 验证配置状态

	yum clean all && yum repolist

![[Pasted image 20241014103128.png]]

