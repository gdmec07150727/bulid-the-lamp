# bulid-the-lamp
centos7下搭建lamp环境，基于阿里云服务器下的
基于阿里云centos7环境下，搭建lamp环境
这次的lamp环境配置，我是在基于centos7的环境下的。当然，我的centos是阿里云里面的镜像，所以这次的php+mysql+apache是安装在阿里云的云服务器ESC上的。

首先，我们先在阿里云购买一个ECS云服务器，选择的是centos7的系统。然后打开我们的实例，在我们的实例那里，选择安全组配置。
 
然后进入到如下页面，点击配置规则。
 
接下来点击添加安全组
 

然后我们需要添加这个80端口的安全组，这样我们才可以访问我们的公网ip
 
然后，阿里云的配置基本完成了。接下来我们可以下载一个ssh工具，比如xshell，用来远程连接我们的阿里云服务器。
 
接下来正式开始配置环境
首先，我们可以执行yum update命令，用以更新yum源。
然后，安装PHP教程如下：
输入指令：yum -y install epel-release（安装epel源）
 
然后，安装php7，
命令：rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm（用以获取php7的源）
 
然后执行命令：yum install php70w php70w-fpm php70w-cli php70w-common php70w-devel php70w-gd php70w-pdo php70w-mysql php70w-mbstring php70w-bcmath（用以安装php7.0）
 
最后，安装成功，然后我们可以检查一下php的版本，命令：php -v
 
接下来，安装mysql
我们这里讲的是通过Mysql的repo源来进行安装，
首先我们得获取repo源: 
命令：wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
下载完后，可以使用ls查看
 

然后接下来，我们来安装：rpm -ivh mysql-community-release-el7-5.noarch.rpm，这条命令是安装刚刚下载得包。
 
然后，就进入正题，开始安装mysql
命令：yum install mysql-community-server
安装成功后，我们可以对mysql设置密码：
首先进入mysql：mysql -u root
 
然后输入指令：set password for 'root'@'localhost' =password(‘root’);
password(‘root’);里的root是你自己定义的密码。
然后，修改成功后，我们可以输入exit退出mysql命令。
在这里要说一下我遇到的坑，我装完mysql后，无法使用指令mysql -u -root进入mysql，然后我的解决方法是，输入指令：systemctl start mysqld（是为了启动mysql的指令）
然后还有重启mysql指令：systemctl restart mysqld
停止mysql指令：systemctl stop mysqld
至此，mysql安装配置就完成了。
接下来安装apache，
执行yum install httpd
然后就直接执行命令启动apache：systemctl start httpd
 

然后我们可以进行我们的第一个php网站的调试。
服务器的根目录是，var/www/html
我们进入到html目录，然后执行vi inf.php命令
进入到vi编辑界面，按i，就可以插入数据了，输入：<?php phpinfo(); ?>
接下来按esc，再按shift+：，输入wq退出并保存，就ok了。
然后我们在浏览器输入公网ip+文件名：xxxxx/inf.php，就显示如下界面了
 









