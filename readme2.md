
CentOS7关闭防火墙（Firewalld ），使用防火墙（iptables）
===
**1、直接关闭防火墙**

systemctl stop firewalld.service； #停止firewall

systemctl disable firewalld.service； #禁止firewall开机启动

**2、安装并启动 iptables service，以及设置开机自启**

yum -y install iptables-services；#安装iptables

systemctl start iptables；#启动iptables

systemctl enable iptables；#自启动iptables

systemctl start ip6tables；#启动ip6tables（不需要可以跳过）

systemctl enable ip6tables；#自启动ip6tables（不需要可以跳过）

**3、配置iptables service**

vi /etc/sysconfig/iptables；#如增加防火墙端口3306和一些常用端口 80、8080等

增加规则：

-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT； -A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT； -A INPUT -p tcp -m state --state NEW -m tcp --dport 8080 -j ACCEPT； 保存退出后。

**4、重启 iptables service**

systemctl restart iptables.service #重启防火墙使配置生效

**5、最后重启系统使设置生效即可**

reboot；
