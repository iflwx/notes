参考文档：https://www.sqlsec.com/2018/05/termux.html

### 一、下载安装

apk下载地址：https://f-droid.org/packages/com.termux/

源码：https://github.com/termux/termux-app

### 二、基本命令

```shell
pkg update   #更新数据源。中间会有停顿询问，直接按回车即可。
pkg list-all  #列出所有可以安装的包
pkg install [package name]   #包安装
pkg uninstall [package name] #包缷载
```

### 三、ipad上远程连接Android

Android上，先安装并启动sshd

```shell
#安装ssh
pkg install openssh
#查看本机root用户名
whoami
#设置密码
passwd
#重启sshd
pkill sshd;sshd
```

ipad端，先安装termius，然后添加Hosts，使用如下设置进行连接：

```ini
Alias: Honor7X(助记名，随便设)
Hostname: 192.168.43.1(Android设备的ip，可用ifconfig查看局域网地址)
Use SSH: Yes
Port: 8022
Username: u0_a171(whoami命令的输出)
Password: 上一步passwd命令设置的密码
```

注意：Android端要允许termux获取wakelock并在前台，ipad端保存termius在前台，否则连接容易断开。

### 四、允许访问手机存储

```shell
# Android6.0以上会弹框确认是否授权，点击"始终允许"后Termux即可访问手机上的文件
termux-setup-storage
```

注意：

1.需在本机输入。

2.授权后，storage文件夹下包含了内置存储的几个文件夹，包括：dcim, downloads, movies, music, pictures, shared。storage下的external-1文件夹对应了外置SD卡上的Android/data/com.termux/files文件夹。

### 五、ngrok内网穿透

1.建立隧道

在网站ngrok.cc上，依次点击：隧道管理 - 开通隧道 - 美国Ngrok免费服务器 - 立即购买

```ini
隧道协议: http
隧道名称: Honor7X(随意)
前置域名: iflwx(需要唯一，最终提供的免费域名为iflwx.free.idcfengye.com)
本地端口: 127.0.0.1:8080(此处端口不要用80，否则自定义程序要监听80端口可能有些困难)
http验证用户名/密码: 为空即可
```

确认后，在"隧道管理"中查看状态。

2.下载python客户端

```shell
pkg install wget
wget https://www.ngrok.cc/sunny/python-ngrok.zip
unzip python-ngrok.zip
```

3.编写并运行ngrok脚本

```shell
#！ /bin/sh
python sunny.py --clientid=XXXXXXXXX &

# 将上面的内容保存，命名为ngrok
./ngrok
```

运行后，控制台有结果日志。也可在"隧道管理"中查看状态。

4.测试方法

```shell
python -m http.server 8080
```

浏览器用http://iflwx.free.idcfengye.com访问验证

### 六、常用软件

```shell
# c
pkg install clang
# python
pkg install python
pkg install vim-python
# node
pkg install nodejs-lts
# go
pkg install golang
# nginx
pkg install nginx
```





