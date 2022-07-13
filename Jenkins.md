## 安装Jenkins碰到的问题
```
jian@jian-VirtualBox:~$   sudo apt-get install jenkins
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
下列【新】软件包将被安装：
  jenkins
升级了 0 个软件包，新安装了 1 个软件包，要卸载 0 个软件包，有 5 个软件包未被升级。
需要下载 90.7 MB 的归档。
解压缩后会消耗 93.5 MB 的额外空间。
获取:1 https://pkg.jenkins.io/debian binary/ jenkins 2.358 [90.7 MB]
已下载 90.7 MB，耗时 37秒 (2,425 kB/s)                                                                                                            
正在选中未选择的软件包 jenkins。
(正在读取数据库 ... 系统当前共安装有 278518 个文件和目录。)
准备解压 .../archives/jenkins_2.358_all.deb  ...
正在解压 jenkins (2.358) ...
正在设置 jenkins (2.358) ...
Job for jenkins.service failed because the control process exited with error code.
See "systemctl status jenkins.service" and "journalctl -xe" for details.
invoke-rc.d: initscript jenkins, action "start" failed.
● jenkins.service - Jenkins Continuous Integration Server
     Loaded: loaded (/lib/systemd/system/jenkins.service; enabled; vendor preset: enabled)
     Active: activating (auto-restart) (Result: exit-code) since Tue 2022-07-12 18:34:09 CST; 4ms ago
    Process: 30945 ExecStart=/usr/bin/jenkins (code=exited, status=1/FAILURE)
   Main PID: 30945 (code=exited, status=1/FAILURE)
dpkg: 处理软件包 jenkins (--configure)时出错：
 已安装 jenkins 软件包 post-installation 脚本 子进程返回错误状态 1
正在处理用于 systemd (245.4-4ubuntu3.17) 的触发器 ...
在处理时有错误发生：
 jenkins
E: Sub-process /usr/bin/dpkg returned an error code (1)
```

## 解决方法
dpkg: 处理软件包xxx(–configure)时出错
由于依赖关系问题 仍未被配置
（个人习惯：root用户进行操作）
解决方法：
第一步：mv /var/lib/dpkg/info /var/lib/dpkg/info_bak 

第二步：mkdir /var/lib/dpkg/info

第三步：apt-get update && apt-get -f install

第四步：mv /var/lib/dpkg/info/* /var/lib/dpkg/info_bak/

第五步：rm -rf /var/lib/dpkg/info

第六步：mv /var/lib/dpkg/info_bak /var/lib/dpkg/info

## 上述方法不是很有用,有用的方法
```
# change user: USER=root
# change port: Environment="JENKINS_PORT=8088"

$ vi /etc/systemd/system/multi-user.target.wants/jenkins.service 

$ apt-get install jenkins

