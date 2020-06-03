
# 版本

frp_0.29.0_linux_amd64.tar.gz  
使用版本 frp_0.29.0_linux_amd64.tar.gz  



# 端口规划
server 端口
7000 frps listen端口
7001 dashboard
9000 gotty
8080 http
9001 vscode --http:www.jiudianren.xyz:9001 paswd vscode
8888  jupyter --http://www.jiudianren.xyz:8888/tree http://www.jiudianren.xyz:8888/lab  passwd 271828
官方版本 使用server端口
pi office
5901 vnc --local 5901
7022 ssh --local 22
7002  static_file ---local none
7003  doccker_unix_sockt----unix.sock
8080-- http--lcoal 8086 --- http://blog.jiudianren.xyz:8080/
pi openfuns 使用的server端口
5902 vnc --local 5901
7023 ssh --local 22
4200 webssh -local 4200
9090 webdash -local 9090
9091  jupyter  -local 9091

http
http://blog.jiudianren.xyz:8080/
9001 vscode
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
- 配置frp 
详见frp文档 
- 测试


frps
https://blog.csdn.net/cao0507/article/details/82758288
https://blog.csdn.net/oxp7085915/article/details/80541032
 
下载：
wget https://github.com/fatedier/frp/releases/download/v0.29.0/frp_0.29.0_linux_amd64.tar.gz  1>lpf 2>&1 &

https://blog.csdn.net/qq_39056805/article/details/80111496
rc.local 需要添加+x 执行权限
/etc/rc.local 下添加 
nohup  /root/frp/frps -c  /root/frp/frps.ini &
nohup  /root/gotty/gotty -p 9000  --credential jiudianren:271828  -w bash &
nohup python3  /home/pi/charge/simplehttpserver.py  -p  8085 &



nohup ./frps -c ./frps.ini &
nohup ./frpc -c ./frpc.ini &
frps.ini
frps.ini
[common]
bind_port = 7000
vhost_http_port=80

dashboard_port = 7500
dashboard_user = jiudianren
dashboard_pwd =271828
max_pool_count = 10
authentication_timeout = 900
subdomain_host =jiudianren.xyz

# console or real logFile path like ./frpc.log
log_file = /home/frp/frps.log
# trace, debug, info, warn, error
log_level = info
log_max_days = 20
#for jianghui 7900-7999


frpc
树莓派
frp_0.13.0_linux_arm.tar.gz 
树莓派用 arm版本
frpc.ini
[common]
#server_addr = 111.231.103.221
server_addr = 106.14.148.245
server_port = 7000
login_fail_exit=false
log_file = /home/frp/frps.log
log_level = info
log_max_days = 10

[ssh]
#ssh -p 7001 pi@111.231.103.221
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port =7001 

[range:vnc]
type = tcp
local_ip = 127.0.0.1
local_port = 5901
remote_port = 5901


[static_file]
type = tcp
remote_port = 7002
plugin = static_file
# 要对外暴露的文件目录
plugin_local_path =/home/pi
# 访问 url 中会被去除的前缀，保留的内容即为要访问的文件路径
plugin_strip_prefix = static_file

[web]
#http://doc.jiudianren.xyz:8080/
type = http
local_port = 8085 
subdomain =doc 

[wrodpress]
type=http
#http://blog.jiudianren.xyz:8080/
local_port=8086
subdomain=blog

[unix_domain_socket]
type=tcp
remote_port=7004
plugin=unix_domain_socket
plugin_unix_path=/var/run/docker.sock
pi@raspberrypi:~$ 
next


openfuns
/home/pi/frp
nohup  /home/pi/frp/frpc  -c   /home/pi/frp/frpc/frpc.ini  &
frpc.ini
[common]                                                                                                                                                                       
server_addr = 106.14.148.245                                                                                                                                                   
server_port = 7000                                                                                                                                                             
log_file=./frpc.log                                                                                                                                                            
log_level = info                                                                                                                                                               
log_max_days =20 
                                                                                                                                                              
[webssh]   
#https:www.jiudianren.xyz:4200                                                                                                                                                                    
type = tcp                                                                                                                                                                     
local_port = 4200                                                                                                                                                              
remote_port=9001                                                                                                                                                               

[ssh]                                                                                                                                                                          
type=tcp                                                                                                                                                                       
local_port=22                                                                                                                                                                  
local_ip=127.0.0.1                                                                                                                                                             
remote_port=7023                                                                                                                                                               
                                                                                                                                                                               
[webdash] 
#https:www.jiudianren.xyz:9090                                                                                                                                                                     
type = tcp                                                                                                                                                                     
local_port = 9090                                                                                                                                                              
remote_port = 9090                                                                                                                                                             
                                                                                                                                                                               
[vscode]    
#https:vscode.jiudianren.xyz:8080                                                                                                                                                                   
type = http                                                                                                                                                                    
local_port = 8081                                                                                                                                                              
subdomain = vscode
                                                                                                                                                             
[jupyter]  
#https:jupyter.jiudianren.xyz:8080                                                                                                                                                                       
type=http                                                                                                                                                                      
local_port = 8888                                                                                                                                                              
subdomain = jupyter

docker run -dit -p 9081:8080 -u root --name vscode -v "/home/pi/mygit:${PWD}" -e PASSWORD=vscode codercom/code-server 

