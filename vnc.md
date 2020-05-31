﻿﻿﻿

1 配置 wifi文件，或者网线连接

#  写空的ssh文件

将SD卡连接到电脑上并打开，直接新建“SSH”文件（无后缀）即可，如下图2




启用远程桌面VNC
同样在命令行内输入sudo apt-get install tightvncserver，为Raspbian安装VNC服务；
安装成功后，输入vncpasswd输入命令设置一个密码。输入两次，然后询问是否设置一个view-only密码，一般不需要，选择n
启动VNC图形界面：vncserver :1 -geometry 1024x768（命令中的:1表示的是1号桌面，我们也可以输入:2创建2号桌面。然后-geometry 1024x768是设置分辨率。按自己需要。）
注意：以root身份开启的vnc桌面和以pi用户身份开启的桌面是不同的。建议大家用pi身份开启就好，也就是命令行最后一个符号是$的时候。
打开之前下载的PC端的VNC客户端，在输入框输入IP地址:桌面号（192.168.0.5:1），点击Connect，此时就进入了Raspbian的桌面。
Enjoy it！


passwd:e





#  开机自启

3. 可选配置
1）设置VNC开机启动
在/etc/init.d/中创建一个文件，例如tightvncserver；
输入'sudo nano /etc/init.d/tightvncserver'；
复制以下内容，在Putty命令行里点击鼠标右键粘贴；
#!/bin/sh
### BEGIN INIT INFO
# Provides:          tightvncserver
# Required-Start:    $local_fs
# Required-Stop:     $local_fs
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Start/stop tightvncserver
### END INIT INFO
# More details see:
# http://www.penguintutor.com/linux/tightvnc

### Customize this entry
# Set the USER variable to the name of the user to start tightvncserver under
export USER=’pi’
### End customization required

eval cd ~$USER
case ”$1” in
  start)
    # 启动命令行。此处自定义分辨率、控制台号码或其它参数。
    su $USER -c ’/usr/bin/tightvncserver -geometry 800x600 :1’
    echo ”Starting TightVNC server for $USER ”
    ;;
  stop)
    # 终止命令行。此处控制台号码与启动一致。
    su $USER -c ’/usr/bin/tightvncserver -kill :1’
    echo ”Tightvncserver stopped”
    ;;
  *)
    echo ”Usage: /etc/init.d/tightvncserver {start|stop}”
    exit 1
    ;;
esac
exit 0
Ctrl+x，存盘退出;
回到命令行做如下配置：
sudo chmod 755 /etc/init.d/tightvncserver
sudo update-rc.d tightvncserver defaults

作者：航航大魔王
链接：https://www.jianshu.com/p/3041f11dcadb
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



vnc:参考这个：

https://www.jianshu.com/p/3041f11dcadb
配置wifi和ssh参考这个：
http://shumeipai.nxez.com/2017/09/13/raspberry-pi-network-configuration-before-boot.html



vnc password jiudianren


https://www.jianshu.com/p/3041f11dcadb
