全局配置比接口配置优先级更高，两者全部配置的话先生效全局的
#全局配置

	spanning-tree portfast bdpufilter default    //开启stp默认bdpu过滤

进入接口

>前置
	spanning-tree portfast//开启边缘端口

	（config-if）#spanning-tree bdpufilter enable    //开启bdpu过滤


#接口配置

      
    （config-if）#spanning-tree bpduguard enable    //开启bdpu过滤