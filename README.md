# BBR2-Kernel
Longterm Project.Update the brand new BBR2 Kernel

感谢stardock制作的Markdown版说明

前星期忍不住入了ikoula 9.9o，然后发现用处不大，平时拿来跑跑转盘和备份，毕竟我的主力机不是这个。  
又看到BBR2新内核居然没人编译RPM包，于是写了个Python脚本，自动git pull+编译RPM和DEB包+git push  
所有内核已经默认开启bbr2和fq，我把bbr2编译进内核了，所以不需要在sysctl切换  

项目地址：  
`https://github.com/gzare/BBR2-Kernel`  


## 最新内核安装方法  

首先开启fq
```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
```

### CentOS7  

```  
mkdir BBR2-Kernel && cd BBR2-Kernel
wget --no-check-certificate https://github.com/gzare/BBR2-Kernel/raw/master/kernel-devel-latest.x86_64.rpm 
wget --no-check-certificate https://github.com/gzare/BBR2-Kernel/raw/master/kernel-latest.x86_64.rpm
wget --no-check-certificate https://github.com/gzare/BBR2-Kernel/raw/master/kernel-headers-latest.x86_64.rpm 
rpm -ivh *.rpm
```  

```  
grub2-set-default 0
grub2-mkconfig -o /boot/grub2/grub.cfg
```  

### Ubuntu/Debian  

```  
mkdir BBR2-Kernel && cd BBR2-Kernel 
wget --no-check-certificate https://github.com/gzare/BBR2-Kernel/raw/master/linux-headers-latest_amd64.deb 
wget --no-check-certificate https://github.com/gzare/BBR2-Kernel/raw/master/linux-image-latest_amd64.deb 
dpkg -i *.deb
update-grub
```  

重启后，查看uname -a查看内核，如果是5.4.0就安装成功。  
更换内核前，请确保VPS拥有VNC功能，若不能启动，请前往VNC页面手动切换内核启动  
本人不能保证是否内核能完美运行  
目前已在Debian10/9 KVM架构和CentOS7 KVM架构上成功重启  


Refer:   
https://www.hostloc.com/forum.php?mod=viewthread&tid=636872&highlight=bbr2  

