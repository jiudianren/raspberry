腾讯主机
111.231.103.221  root:
2 云主机
111.231.103.221  root  centos#123
cat /proc/meminfo 查看内存
cat /proc/cpuinfo| grep "physical id"| sort| uniq| w
阿里主机 Lpfe.
root/Lpf2.71828
yum install python3  安装python3 
yum install python3-pip 安装 pip
python2和python3 并存是使用
python3 -m pip install XXX  安装软件
python3 -m pip uninstall jupyterlab
python3 -m pip install jupyterlab

git 配置
1、打开git bash。
 2、使用cd ~/.ssh可以查看是否已配置SSH。
 3、执行生成公钥和私钥的命令ssh-keygen -t rsa 并按回车3下（为什么按三下，是因为有提示你是否需要设置密码，如果设置了每次使用Git都会用到密码，一般都是直接不写为空，直接回车就好了）。会在一个文件夹里面生成一个私钥 id_rsa和一个公钥id_rsa.pub。（可执行start ~命令，生成的公私钥在 .ssh的文件夹里面）。
 4、.ssh如果不做特殊处理的话，一般是在C:\Users\Administrator目录下。如果看不到.ssh文件，可以使用ls -ah指令查看隐藏文件夹即可，这是存放秘钥的文件，打开这个文件会看到id_rsa和id_rsa.pub。id_rsa是私钥文件，id_rsa.pub是公钥文件。
 5、执行查看公钥的命令cat ~/.ssh/id_rsa.pub  。



备案网
http://www.beian.gov.cn/apply/subject?token=164349b3-0b3d-4357-a027-d106a30bc456

https://cloud.tencent.com/document/product/243/19142
环境修复
https://www.cnblogs.com/mashuqi/p/10955089.html

https://blog.csdn.net/codeLife1993/article/details/89679586

https://blog.csdn.net/zhangdongren/article/details/82685932


 # ssh

 mobaxterm


 开启 云主机 ftp
https://cloud.tencent.com/document/product/213/10912
#### passive
https://www.jb51.net/article/36917.htm
## ftp
winscp
root:centos#123
passive
https://www.jb51.net/article/36917.htm
ftp 命令
https://www.cnblogs.com/feiquan/p/9236768.html

六、nohup 命令
还有比disown更方便的命令，就是nohup。

$ nohup node server.js &
nohup命令对server.js进程做了三件事。
阻止SIGHUP信号发到这个进程。
关闭标准输入。该进程不再能够接收任何输入，即使运行在前台。
重定向标准输出和标准错误到文件nohup.out。
也就是说，nohup命令实际上将子进程与它所在的 session 分离了。
注意，nohup命令不会自动把进程变为"后台任务"，所以必须加上&符号。


nohup python xxxx &


修改ssh端口
https://cloud.tencent.com/developer/article/1183274
https://cloud.tencent.com/developer/article/1183274

搭建 webshell
https://blog.csdn.net/pariese/article/details/78742277


子账户：

https://jingyan.baidu.com/article/f00622284cfb16fbd3f0c8bc.html


webshell
https://cloud.tencent.com/document/product/213/5436

webssh
https://www.cnblogs.com/franknihao/p/8963634.html

https://cloud.tencent.com/document/product/213/8044

公网ip:
https://cloud.tencent.com/document/product/213/17940
云主机通过ifconfig 是看不到 主机ip的。 

https://cloud.tencent.com/document/product/213/4934

https://shimo.im/docs/bum6gVwxtYM5w8Vi/ 「server」，可复制链接后用石墨文档 App 或小程序打开


jiudianren.xyz

https://github.com/jiudianren/mypy/blob/master/serverTest/server.py

https://segmentfault.com/a/1190000016182652

ftp
https://blog.csdn.net/zhuweideng/article/details/80817784
安装python3
https://www.cnblogs.com/linga/p/9442126.html



图片: https://uploader.shimo.im/f/usgWxoSBAaAjTXMb.png






