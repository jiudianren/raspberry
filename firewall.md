
查看centos版本
https://blog.csdn.net/shuaigexiaobo/article/details/78030008
https://www.cnblogs.com/Pynix/p/11803071.html
https://github.com/cdr/code-server
cat /etc/issue
 cat /etc/redhat-release
防火墙 
https://blog.csdn.net/s_p_j/article/details/80979450

查看防火墙是否开启

Centos7 开启 , 关闭端口 
CentOS7 默认没有使用iptables , 所以不能通过编辑 iptables 的配置文件来开启端口 , CentOS7 采用了 firewalld 防火墙 
如要查询是否开启3306端口则 : 
firewall-cmd -query-port=3306/tcp
# firewall-cmd –query-port=3306/tcp 
开启端口 : 
# firewall-cmd –zone=public –add-port=3306/tcp –permanent 
命令含义 : –zone #作用域 , –add-port=80/tcp #添加端口 , 格式为 : 端口/通讯协议 , –permanent #永久生效 , 没有此参数重启后失效 
重启防火墙 : 
# firewall-cmd –reload 
关闭端口 : 
# firewall-cmd –zone=public –remove-port=3306/tcp –permanent

Centos6.X 开启 , 关闭端口 
使用 iptables 开放如下端口 : 
# /sbin/iptables -I INPUT -p tcp –dport 3306 -j ACCEPT 
保存 : 
# /etc/rc.d/init.d/iptables save 
重启服务 : 
# /etc/rc.d/init.d/iptables restart 
查看端口是否开放 : 
# /etc/init.d/iptables status 
关闭端口 : 
# /sbin/iptables -I INPUT -p tcp –dport 3306 -j DROP