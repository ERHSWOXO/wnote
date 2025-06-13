
# 安装AD CS 服务

![[Pasted image 20240818164516.png]]

# 配置AD CS 服务

没图片

让右上角的小旗子的黄色图标消失

# 导出CA服务器的私钥

## 打开mmc工具

	win+r 输入mmc

![[Pasted image 20240818164814.png]]
## 打开计算机证书
![[Pasted image 20240818165033.png]]
![[Pasted image 20240818165107.png]]
![[Pasted image 20240818165133.png]]
## 找到CA的根证书
![[Pasted image 20240818165233.png]]
## 导出
![[Pasted image 20240818165256.png]]
![[Pasted image 20240818165327.png]]
下一步下一步
![[Pasted image 20240818165419.png]]
导出完成
![[Pasted image 20240818165438.png]]

# 到要去信任的机器上
## 双击打开，在输入密码，在选择路径的时候要选择受信任的颁发机构
![[Pasted image 20240818165636.png]]
## 导入成功后去要去信任的机器上查看
![[Pasted image 20240818165920.png]]
可以看到现在已经有CA的根证书了