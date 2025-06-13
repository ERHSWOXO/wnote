#操作系统：Fedora-Server-40 
# 安装软件包
```
yum install mysql mysql-server.x86_64 mysql-libs.x86_64  -y
```
# 启动服务
```
systemctl start mysqld.service
```
# 配置服务自启动
```
systemctl enable mysqld.service 
```