# my operator

docker run -itd --name nctest -p  8888:80 -v  /srv/dev-disk-by-label-Elements/nextcloud:/var/www/html/   nextcloud

admin/e
Docker+Nextcloud快速部署个人网盘

https://www.cnblogs.com/Timesi/archive/2018/09/21/9688463.html






https://blog.csdn.net/jdyanghang/article/details/102828553


openmediavault


由于我把目录挂载到了移动硬盘下,而移动硬盘用得又是NTFS文件系统,并不支持直接设置0770权限.(据说可以指定ntfs挂载参数来解决,嫌麻烦就没有实践)
搜索引擎一波之后在nextcloud的github上inuse中找到了解决方案:https://github.com/nextcloud/server/issues/3245
遂准备按照上面给出的方法修改代码,然而翻代码发现新版已经加入了选项支持,不需要再修改核心代码了.
只要在nextcloud目录下config/config.php文件中加入

'check_data_directory_permissions' => false


https://blog.csdn.net/u010476430/article/details/89205028


'trusted_domains' =>
  array (
    0 => 'nextcloud.jiudianren.xyz:8080','192.168.31.138',
  ),



 array (
    'demo.example.org',
    'otherdomain.example.org',
  ),





错误 #0:
OMV\ExecException: Failed to execute command 'export PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin; export LANG=C.UTF-8; mount -v --source '/dev/disk/by-label/Elements' 2>&1' with exit code '13': $MFTMirr does not match $MFT (record 0).
Failed to mount '/dev/sda1': Input/output error
NTFS is either inconsistent, or there is a hardware fault, or it's a
SoftRAID/FakeRAID hardware. In the first case run chkdsk /f on Windows
then reboot into Windows twice. The usage of the /f parameter is very
important! If the device is a SoftRAID/FakeRAID then first activate
it and mount a different device under the /dev/mapper/ directory, (e.g.
/dev/mapper/nvidia_eahaabcc1). Please see the 'dmraid' documentation
for more details. in /usr/share/php/openmediavault/system/process.inc:182
Stack trace:
#0 /usr/share/php/openmediavault/system/filesystem/filesystem.inc(738): OMV\System\Process->execute()
#1 /usr/share/openmediavault/engined/rpc/filesystemmgmt.inc(930): OMV\System\Filesystem\Filesystem->mount()
#2 [internal function]: Engined\Rpc\OMVRpcServiceFileSystemMgmt->mount(Array, Array)
#3 /usr/share/php/openmediavault/rpc/serviceabstract.inc(123): call_user_func_array(Array, Array)
#4 /usr/share/php/openmediavault/rpc/rpc.inc(86): OMV\Rpc\ServiceAbstract->callMethod('mount', Array, Array)
#5 /usr/sbin/omv-engined(537): OMV\Rpc\Rpc::call('FileSystemMgmt', 'mount', Array, Array, 1)
#6 {main}