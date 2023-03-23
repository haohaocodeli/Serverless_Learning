## 快速搭建LAMP环境

在Web Terminal中，使用yum命令安装Apache服务及其扩展包。

说明：扩展包包括httpd-manual、mod_ssl、mod_perl、mod_auth_mysql。成功安装后，返回类似如下图结果，则表示Apache服务及其扩展包安装成功。

Apache是世界使用排名第一的Web服务器软件。它可以运行在几乎所有广泛使用的计算机平台上，由于其跨平台和安全性被广泛使用，是最流行的Web服务器端软件之一。

1. 在页面右侧，单击****![](https://img.alicdn.com/imgextra/i1/O1CN015uuW5n1hahPJ6SPRb_!!6000000004294-2-tps-25-21.png)图标，切换至Web Terminal。

![](https://ucc.alicdn.com/pic/developer-ecology/4608318dd5fb424e95d97a606bd03e0c.jpeg)

2. 执行如下命令，安装Apache服务及其扩展包。

```
yum -y install httpd httpd-manual mod_ssl mod_perl mod_auth_mysql
```

返回类似如下图结果则表示安装成功。

![](https://img.alicdn.com/imgextra/i3/O1CN01kN6tv41m6XOxSDQHr_!!6000000004905-2-tps-1271-240.png)

3. 执行如下命令，启动Apache服务。

```
systemctl start httpd.service
```

4、 在本地电脑的浏览器的址栏中，输入ECS公网登录地址，并按Enter键。

若返回页面如下图所示，说明Apache服务启动成功。

![](https://ucc.alicdn.com/pic/developer-ecology/39b506798c2344948ec193656805fcd1.jpeg)

3. 安装并配置MySQL

MySQL是最流行的关系型数据库管理系统，在WEB应用方面MySQL是最好的 RDBMS(Relational Database Management System：关系数据库管理系统)应用软件之一。

1. 执行以下命令，下载并安装MySQL官方的Yum Repository。

```
wget http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql-community-server --nogpgcheck
```

2. 运行以下命令查看MySQL版本号。

```
mysql -V
```

返回结果如下所示，表示MySQL安装成功。

![](https://img.alicdn.com/imgextra/i4/O1CN01J4gXUw1FSdBkMlWsT_!!6000000000486-2-tps-638-41.png)

3. 执行以下命令，启动 MySQL 数据库。

```
systemctl start mysqld.service
```

4. 执行以下命令，查看MySQL初始密码。

```
grep "password" /var/log/mysqld.log nqzzlwPeh0/w
```

![](https://img.alicdn.com/imgextra/i4/O1CN01BwpBDN20gAqCNUGUd_!!6000000006878-2-tps-855-39.png)

5. 执行以下命令，登录数据库。

```
mysql -uroot -p
```

![](https://img.alicdn.com/imgextra/i3/O1CN01b3xc211osHvUKh4j0_!!6000000005280-2-tps-748-233.png)

6. 输入MySQL的初始密码。

说明：在输入密码时，界面不会显示密码。

![](https://ucc.alicdn.com/pic/developer-ecology/y4dn6eatoa22k_9776b4bb4c6d4db3a7fc89a327b6af6a.png)

7. 执行以下命令，修改MySQL默认密码。

```
set global validate_password_policy=0;  #修改密码安全策略为低（只校验密码长度，至少8位）。
ALTER USER 'root'@'localhost' IDENTIFIED BY '12345678';
```

![](https://img.alicdn.com/imgextra/i1/O1CN01xFGaMC1MiO7qHTfRk_!!6000000001468-2-tps-537-104.png)

8. 执行以下命令，授予root用户远程管理权限。

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '12345678';
```

![](https://img.alicdn.com/imgextra/i4/O1CN01E5xGTI1wcjOsp3jzp_!!6000000006329-2-tps-619-45.png)

9. 输入exit退出数据库。

![](https://img.alicdn.com/imgextra/i2/O1CN01CeroXp1SAOQ4Lta4v_!!6000000002206-2-tps-112-42.png)

4. 安装PHP

PHP（PHP：Hypertext Preprocessor递归缩写）中文名字是：“超文本预处理器”，是一种广泛使用的通用开源脚本语言，适合于Web网站开发，它可以嵌入HTML中。编程范型是面向对象、命令式编程的。

1. 执行以下下命令，安装PHP环境。

```
yum -y install php php-mysql gd php-gd gd-devel php-xml php-common php-mbstring php-ldap php-pear php-xmlrpc php-imap
```

![](https://img.alicdn.com/imgextra/i1/O1CN013afzBr1SMl7929gPq_!!6000000002233-2-tps-1271-331.png)

2. 执行以下命令创建PHP测试页面。

```
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```

![](https://img.alicdn.com/imgextra/i2/O1CN01SzmdoM1MHMklaiUDx_!!6000000001409-2-tps-715-26.png)

3. 执行以下命令，重启Apache服务。

```
systemctl restart httpd
```

![](https://img.alicdn.com/imgextra/i3/O1CN0154Y5oJ1hR55dqFm4e_!!6000000004273-2-tps-475-24.png)

4. 在本地浏览器的址栏中，，访问[http://ecs公网ip](http://%3CECS%E5%85%AC%E7%BD%91IP)

[![](https://img.alicdn.com/imgextra/i4/O1CN01UkJF1I1VPSIKnFRsU_!!6000000002645-2-tps-472-758.png)git@github.com:haohaocodeli/Serverless_Learning.git](http://%3CECS%E5%85%AC%E7%BD%91IP)

5. 安装phpMyAdmin

phpMyAdmin是一个MySQL数据库管理工具，通过Web接口管理数据库方便快捷。

1. 执行以下命令，创建phpMyAdmin数据存放目录。

```
mkdir -p /var/www/html/phpmyadmin
```

![](https://img.alicdn.com/imgextra/i3/O1CN01A6N8Ym1Dxempo5Bo3_!!6000000000283-2-tps-682-28.png)

2. 执行以下命令，下载phpMyAdmin压缩包。

```
wget --no-check-certificate https://labfileapp.oss-cn-hangzhou.aliyuncs.com/phpMyAdmin-4.0.10.20-all-languages.zip
```

![](https://img.alicdn.com/imgextra/i4/O1CN01BqOCCw2780bdxChYD_!!6000000007751-2-tps-1291-204.png)

3. 执行以下命令，安装unzip并解压phpMyAdmin压缩包。

```
yum install -y unzip
unzip phpMyAdmin-4.0.10.20-all-languages.zip
```

4. 执行以下命令，复制phpMyAdmin文件到数据存放目录。

```
mv phpMyAdmin-4.0.10.20-all-languages/*  /var/www/html/phpmyadmin
```

5. 在本地浏览器的址栏中，输入[http://实例公网](http://%E5%AE%9E%E4%BE%8B%E5%85%AC%E7%BD%91) IP/phpmyadmin，访问phpMyAdmin。

返回页面如下图所示，说明phpMyAdmin安装成功。

![](https://img.alicdn.com/imgextra/i2/O1CN01WVgI1m1C6hNDDatqj_!!6000000000032-2-tps-620-570.png)

9. 在phpMyAdmin登录页面，依次输入MySQL的用户名和密码，单击执行。

![](https://img.alicdn.com/imgextra/i4/O1CN01lXqT5q1TPnM52zgwD_!!6000000002375-2-tps-556-614.png)

返回页面如下图所示，表示MySQL连接成功。

![](https://img.alicdn.com/imgextra/i3/O1CN018cHAcS1OkL2eEhHfT_!!6000000001743-2-tps-1313-776.png)
