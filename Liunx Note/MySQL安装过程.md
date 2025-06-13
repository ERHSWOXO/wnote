#操作系统：Debian12-6
由于debian 官方从11开始不使用mysql改用mariadb
所以
# 从官网下载安装包
https://dev.mysql.com/downloads/repo/apt/
>看清楚安装包的名称
```
wget https://dev.mysql.com/get/mysql-apt-config_0.8.32-1_all.deb
```
# 安装deb包

```
dpkg -i mysql-apt-config_0.8.32-1_all.deb
```
#### 选择第一个
![[Pasted image 20240902103528.png]]
#### 选择lts和8.0都可以
![[Pasted image 20240902103618.png]]
#### 选择ok
![[Pasted image 20240902103528.png]]
# 更新apt源
```
apt update 
```

>如果是debian11

>如果是debian11

# 安装mysql-server
```
apt install mysql-server  -y
```

# 安装完成后查看服务状态

```
systemctl status mysql.service
```