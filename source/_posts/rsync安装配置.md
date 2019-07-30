## rsync 同步文件到服务器

### Linux命令

		安装
		yum install -y rsync

		查看服务器进程 		
		ps aux | grep rsync

		杀死进程
		pkill rsync

		启动服务
		rsync --daemon --config=/etc/rsyncd.conf

		设置权限
		chmod 600 /etc/rsyncd.passwd
		chown -R publish:publish 目录

### 服务端
	    创建传输目录

### 服务端配置文件

		$ vi /etc/rsyncd.conf

		#全局配置
		uid = root
		gid = root
		incoming chmod = Du=rwx,Dog=rx,Fu=rwx,Fgo=rx
		exclude = node_modules/ .git/

		# 模块配置
		[www]    
		host allow = *
		path = /home/wwwroot
		comment = www
		auth users = publish
		secrets file = /etc/rsyncd.passwd
		read only = no

### 服务端密码文件

		$ vi /etc/rsyncd.passwd

		user:passwd   // publish:abc123

### 客户端

		安装
		windows版本

		项目文件模板
		- publish
		  - pubToProd.sh
		  - PwdPubToProd.pwd
		
		// pubToProd.sh

		echo '*************发布正式环境******************'
		echo '*                                         *'
		echo '*         地址: 95.163.202.221             *'
		echo '*         密码: 隐藏                       *'
		echo '*                                         *'
		echo '*******************************************'
		echo '                                           '
		echo '*              starting...                *'
		echo '                                           '
		echo -n " 确认发布到正式环境!!!!!!请输入(yes) -> "
		read int
		if [[ "$int" == "yes" || "$int" == "y" ]]; then

    		echo '                                           '
    		echo '                                           '
    		rsync -aP --progress  --password-file=./PwdPubToProd.pwd ../dist/ publish@95.163.202.221::www/test.yeyanjie.com/node-react-admin

    		echo '                                           '
    		echo '                                           '
    		echo '******************END**********************'
    		echo '                                           '
		else
    		echo '                                           '
    		echo '                                           '
    		echo '*******************************************'
    		echo '*                                         *'
    		echo -e '*     \033[31m    确认失败,请重新发布！ \033[0m          *'
    		echo '*                                         *'
    		echo '*******************************************'
		fi

		// PwdPubToProd.pwd
		passwd