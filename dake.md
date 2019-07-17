# Linux系统下mysql的安装（以deepin系统为示范）

标签（空格分隔）： 教程 mysql

---
## 简介 ##
MySQL是关系性数据库管理系统，有瑞典Mysql AB 公司目前属于 Oracle 旗下产品。MySQL 是最流行的关系型数据库管理系统之一，在 WEB 应用方面，MySQL是最好的 RDBMS (Relational Database Management System，关系数据库管理系统) 应用软件之一。
## 下载 ##

> https://dev.mysql.com/downloads/file/?id=486006
## 安装 ##
打开命令行终端按照一下步骤输入

 1. 创建组  

> shell>groupadd mysql

  (mysql可以自定义)
 2. 创建用户 

> shell>useradd -r -g mysql -s /bin/false mysql

 3. 选择安装目录 

> shell>cd /home/user

 可以自定义安装目录
 4. 解压  

> shell>tar xvf /path/to/mysql-VERSION-OS.tar.xz

 (可以直接把压缩包复制到/home/user目录左键选择解压）
 5. 创建一个指向安装目录的符号链接 

> shell>ln -s full-path-to-mysql-VERSION-OS mysql

 6. 配置环境变量 

> shell>export PATH=$PATH:/usr/local/mysql/bin

## 验证 ##
打开命令行终端输入

> shell>mysqladmin --version

如果显示如下则安装完成：

> mysqladmin  Ver 8.0.16 for linux-glibc2.12 on x86_64 (MySQL Community
> Server - GPL)



