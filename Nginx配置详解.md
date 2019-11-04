# Nginx配置详解

关键字（空格分隔）： 教程 nginx服务器

---
## 简介 ##

## nginx配置文件结构分析 ##

nginx的配置文件位于其安装目录安装之下
nginx.conf由多个模块组成最外面的是main，其中main包括evnets和http，http又包括upstream和多个server，server又可以包含多个location。
## 注释 ##
main：全局配置，main块设置指令将影响其他的设置
server：主机配置，主机配置主要用于指定主机和端口
upstream：负载均衡配置，用于一系列后端服务器设置
location：主要用于配置页面的位置

##关系##

server继承main，location继承server，upstream既不会继承其他设置也不会被继承。在这四个部分当中，每个部分都包含若干指令，这些指令主要包含Nginx的主模块指令、事件模块指令、HTTP核心模块指令，同时每个部分还可以使用其他HTTP模块指令，例如Http SSL模块、HttpGzip Static模块和Http Addition模块等。

##main##
user：指定nginx worker的工作用户和工作组，默认是nobody，
worker processor：指定要开放的进程数量
error log：指定错误文件
pid：指定进程pid的存放文件位置
worker_rlimit_nofile：用于绑定worker进程和CPU，Linux内核2.4以上可用
## nginx内置变量 ##
$host:请求中的主机头字段，如www.google.com，如果请求的主机字段为空或者不可用，则为处理请求的server名称
$http_(header):http请求头中的内容，header为http请求内容的小写，如$http_user_agent为User-Agent的值
$remote_addr:客户端的ip地址
$remote_port:客户端的端口
$request_method:请求的方法
$request_uri:包含了一些原始参数的uri
$scheme:所用的协议，例如http或者https
$server_name:服务器的名字
$server_port:请求到达客户端的端口号
$server_protocol:请求使用的协议，通常是http/1.0或者http/1.1
$uri:请求中的当前uri
$http_origin:浏览器携带的origin头
## if语句 常用的正则 ##
= != :比较的一个变量和字符串
～ ！* :与正则表达式匹配的变量，如果这个正则表达式中包含
-f ！-f：检查一个文件是否存在
-d ！-d：检查一个目录是否存在
-e ！-e：检查一个文件，目录，符号链接是否存在
-x ！-x：检查一个文件是否可执行
