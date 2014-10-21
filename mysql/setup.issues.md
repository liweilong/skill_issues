# MySQL安装配置 #

## ubuntu 安装、卸载、重装 ##
### 安装 ###
---
	sudo apt-get install mysql-server
### 配置（允许局域网内远程访问） ###
---
	1.	授权外部访问:  
		进入mysql控制台：  
		mysql -u root -p   
		授予权限：  
		GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'yourpasswd' WITH GRANT OPTION;
		刷新权限：  
		flush privileges;
	2.	防火墙开放端口:  
		sudo iptables -A INPUT -p tcp --dport 3306 -j ACCEPT
	3.	编辑配置文件跳过域名逆向解析:  
		vim /etc/mysql/my.conf
		在`[mysqld]`下添加：  
		skip-host-cache
		skip-name-resolve
### 卸载 ###
---
	sudo apt-get purge mysql-server
	sudo apt-get autoremove
	删除相应文件夹：
	rm -rf /usr/lib/mysql/
	rm -rf /usr/share/mysql