#系统环境：Centos7 
# 把默认的repo文件移至/tmp

	mv /etc/yum.repos.d/* /tmp
# 创建网络repo文件

	 vi /etc/yum.repo.d/ftp.repo
# 编辑
![[Pasted image 20241014103900.png]]
# 验证配置状态

	yum clean all && yum repolist

![[Pasted image 20241014104000.png]]
