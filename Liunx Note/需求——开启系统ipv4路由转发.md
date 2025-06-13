# 编辑 /etc/sysctl.conf 文件

```
vim /etc/sysctl.conf 
```

# 找到第28行，取消注释

```
net.ipv4.ip_forward=1
```

# 确认配置生效

```
root@debian:~# sysctl -p
net.ipv4.ip_forward = 1
```