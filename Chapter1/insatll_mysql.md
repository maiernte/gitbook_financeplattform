# MySQL 数据库

## 安装数据库

下载并安装[MySQL](https://dev.mysql.com/downloads/mysql/)。完成后打开Mac的`偏好设置`，运行数据库。服务器上用命令行安装

```sh
$ sudo apt-get install mysql-server
$ sudo apt-get install mysql-client
安装时输出root用户的密码
```

为系统设置命令路径。

```sh
PATH="$PATH":/usr/local/mysql/bin
```

在Mac系统下每次重启终端都要重新给PATH赋值，要把它保存到设置文件中。

```sh
mysql -V
zsh: command not found
cd ~
sudo vim .bash_profile
# 加入这行
export PATH=${PATH}:/usr/local/mysql/bin/
保存退出后
source ~/.bash_profile
```

并用密码登陆到根用户

```
mysql -u root -p
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.01 sec)

mysql> select * from mysql.user;
# 运行退出命令
```

## 配置用户权限

配置服务器端的访问权限，请看另外一篇文章 [配置服务器段MySQL](https://goldentianya.pub/wiki/config-mysql-access-privileges-on-vps.html)。但如果安装了 phpmyadmin 则没有必要了。因为不需要从外部直接访问数据库。将来客户端的软件要读取数据的话，也只能通过 web service 接口。

## 重设密码

mac 上先通过`偏好设置`停止数据库运行，在终端输入

```sh
cd /usr/local/mysql/bin/
# 回车后登录管理员权限
sudo su
# 回车后输入以下命令来禁止mysql验证功能
./mysqld_safe --skip-grant-tables &
# 回车后mysql会自动重启（偏好设置中mysql的状态会变成running）
# 运行以下命令
./mysql
FLUSH PRIVILEGES
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('你的新密码');
```

## 管理后台 phpmyadmin

```sh
$ sudo apt-get install phpmyadmin
$ sudo apt-get install php-mbstring
$ sudo apt-get install php-gettext
# 安装时选择自动配置数据库，输入数据库root账号的密码
# 如果不安装以上两个php软件包，则会报错或者白屏，提示找不到/usr/share/php/php-gettext/gettext.inc之类的错误
```

- 对于服务器选择，请选择apache2 。
- 当询问是否使用dbconfig-common设置数据库时，选择yes
- 然后您将被要求选择并确认phpMyAdmin的MySQL应用程序密码 , 用户名是 `phpmyadmin`

```sh
# 建立/var/www/html 下的软连接
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
```

安装过程将phpMyAdmin Apache配置文件添加到`/etc/apache2/conf-enabled/`目录中，并在该目录中自动读取。 我们唯一需要做的就是明确地启用`mbstring` PHP扩展，我们可以通过键入以下命令来实现：

```
sudo phpenmod mbstring
```

之后，您需要重新启动Apache才能识别您的更改：

```
sudo systemctl restart apache2
```

您现在可以通过访问服务器的域名或公共IP地址，然后访问`/phpmyadmin`来访问Web界面：

```sh
https://your_domain_or_IP/phpmyadmin
# https://217.160.61.19/phpmyadmin
```

命令行登陆，查看用户 `phpmyadmin` 的权限

```mysql
mysql> show grants for phpmyadmin@localhost;
```

> +--------------------------------------------------------------------+
> | Grants for phpmyadmin@localhost                      |
> +--------------------------------------------------------------------+
> | GRANT USAGE ON *.* TO 'phpmyadmin'@'localhost'                     |
> | GRANT ALL PRIVILEGES ON `phpmyadmin`.* TO 'phpmyadmin'@'localhost' |
> +--------------------------------------------------------------------+
> 2 rows in set (0.00 sec)

