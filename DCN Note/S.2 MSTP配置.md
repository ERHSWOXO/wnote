	spanning-tree     //开启MSTP功能

	spanning-tree mst configuration    //进入MSTP配置模式

	mstp-region)#name [MSPT域名]    //配置MSTP域名

	mstp-region)#revision-level 1    //配置MSTP版本

	mstp-region)#instance 1 vlan [要绑定的VLAN]

	mstp-region)#instance 2 vlan [要绑定的VLAN]

	spanning-tree mode mstp    //配置生成树模式为MSTP

	#spanning-tree mst 1 priority 24576\root primary //配置优先级或者直接设置主备

	#spanning-tree mst 2 priority 28672\root secondary //配置优先级或者直接设置主备