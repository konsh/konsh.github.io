---
title: Mac本地安装MySQL
date: 2022-12-06 11:46:45
tags: 
    - MacOS
    - MySQL
category: 开发
keywords: MacOS, MySQL
description: 本地搭建一个MySQL数据库。
cover: 
---

# 前提
Mac上安装MySQL的方式有两种：brew安装、安装包安装


# brew按照MySQL
在MacOS上，最便捷的安装方式就是通过brew按照MySQL。

## 安装MySQL
```
brew install mysql
```

## 启动MySQL服务器
```
brew services start mysql
```

## 配置MySQL服务器
按照提示运行以下命令配置MySQL服务器（安全性）
```
mysql_secure_installation
```
此配置过程中，可以设置root密码，配置一些选项一增强MySQL服务器的安全性。
```
Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD COMPONENT can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD component?

Press y|Y for Yes, any other key for No: Y

There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 0
Please set the password for root here.

New password:

Re-enter new password:

Estimated strength of the password: 25
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y
Success.


Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y
Success.

By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y
 - Dropping test database...
Success.

 - Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y
Success.

All done!
```

## MySQL服务器一些管理命令
- brew services start mysql 启动MySQL服务器，并设置为自启动
- brew services stop mysql 停止MySQL服务器，并设置为非自启动
- mysql.server start 启动MySQL服务器
- mysql.server stop  停止MySQL服务器

在配置过程中若遇到配置失败，或是异常报错的情况 PS：我遇到的情况是```brew install MySQL unknown or unsupported macOS version: :dunno```，在更新brew后依旧报错。最终发现原来是brew配置问题（源被我换成了阿里源），最后还是恢复默认设置后就没有再遇到报错。


# 安装包安装MySQL
安装包安装有UI界面，对于不擅长使用命令行的用户来说更加友好。

## 下载安装包
通过MySQL社区版下载dmg文件，该文件包含了MySQL的安装器：[点击这里](https://dev.mysql.com/downloads/mysql/)

## 安装MySQL
下载安装包后，按照提示点击安装即可。