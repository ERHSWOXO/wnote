# 编辑sshd配置文件

```
vim /etc/ssh/sshd_config
```
# 将第34行修改为

```
PermitRootLogin yes
```

# 重启服务

```
systemctl restart sshd
```

# 就可以远程链接了
