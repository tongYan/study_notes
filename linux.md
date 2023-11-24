

# 快捷键

Ctrl + R  // 输入快捷键后，可以搜索并执行之前输入过的命令



## 系统信息

- uname -r  查看内核信息

- cat /etc/redhat-release  系统版本

- lscpu    查看cpu信息

- df   -h   查看空间使用情况

   





# 用户管理

## 创建用户  

 `useradd yan`

可在/etc/passwd  /etc/shadow文件中查看

使用命令`id yan`   uid=1000(yan) gid=1000(yan) 组=1000(yan)

用户的家目录 /home/yan

设置用户密码 `passwd yan`

## 删除用户

userdel yan     //此时/home/yan目录没有删除

userdel  -r yan     // 彻底删除、/home/yan目录删除



修改用户 usermod



## su与sudo

su     切换用户  

sudo 	以其他用户身份执行命令

visudo		设置需要使用sudo的用户（组），在文件中添加 `yan ALL=/sbin/shutdown -c` 表示yan可以通过sudo执行`/sbin/shutdown -c`命令，此时输入yan的密码





# 网络

**网络状态查看**

net-tools    老版本工具

- ifconfig
- route
- netstat

iproute	iproute2   centos7+主推工具

- ip
- ss



**ifconfig**

```
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.63  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::f816:3eff:fef6:4e8d  prefixlen 64  scopeid 0x20<link>
        ether fa:16:3e:f6:4e:8d  txqueuelen 1000  (Ethernet)
        RX packets 11560  bytes 2146614 (2.0 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 9024  bytes 1912338 (1.8 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```

eth0  第一块网卡（网络接口），centos7使用了一致性网络设备命名

你的第一个网络接口可能叫做下面的名字

- eno1	板载网卡
- ens33  PCI-E网卡
- enp0s3  无法获取物理信息的PCI-E网卡
- 以上都不匹配则使用eth0



网卡命名规则受biosdevname和net.ifnames两个参数影响

- 编辑/etc/default/grub 文件，增加biosdevname=0 net.ifnames=0
- 更新 grub    grub2-mkconfig -o /boot/grub2/grub.cfg
- 重启生效  reboot



## 网络故障排除

- ping   		  检测当前主机到目标主机是否畅通
- traceroute     追踪路由，追踪每一跳、检测网络质量
- mtr                检测是否有数据包丢失
- nslookup     查看域名访问对应的ip
- telnet           检查端口连接状态
- tcpdump      分析数据包
- netstat          服务监听范围
- ss                类似netstat



## 网络服务管理

网络服务管理分为两种，分别为sysv 和systemd

service network start|stop|restart

chkconfig --list network      chkconfig --level  2345 network off



systemctl  start|stop|restart|status  NetworkManager

systemctl  enable|disable  NetworkManager



网卡配置文件： /etc/sysconfig/network-scripts/





配置文件

ifcfg-eth0

/etc/hosts





# 软件包管理

## rpm

- rpm包格式

  vim-common-7.4.10-5.el7.x86_64.rpm      mysql80-community-release-el7-11.noarch.rpm

  - 软件名称  vim-common
  - 软件版本 7.4.10-5
  - 系统版本 el7   代表Linux7/centos7版本     `uname -r`查看内核信息
  - 平台 x86_64     *noarch*是no architecture的意思，任何平台通用

- rpm命令参数

  - -q 	查询软件包.    `rpm -qa` 查询系统所以安装的包 
  - -i      安装
  - -e     卸载



## yum

- yum配置文件 /etc/yum.repos.d/CentOS-Base.repo







# grub

启动引导软件

grub配置文件

- /etc/default/grub   基本设置
- /etc/grub.d              详细设置
- /boot/grub2/grub.cfg 
- grub2-mkconfig  -o  /boot/grub2/grub.cfg 





# 进程管理

## 查看进程

- ps
- pstree   树形结构查看
- top



## 进程通信方式——信号

## 守护进程和系统日志

