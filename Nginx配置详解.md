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