---
title: 操作系统查看端口占用及结束进程方法
date: 2022-06-17 15:30:11
category: 开发
tags: [MAC, Linux,  Windows]
keywords: 进程,查看进程,系统,端口占用
description: Windows/Mac/Linux操作系统查看端口占用及结束进程方法
---

本地开发程序时经常会碰到端口占用的情况，这个时候就需要使用命令查看并将占用的进程杀掉。以下是不同操作系统的不同查询方式。
示例：
    查询端口4000的占用情况，占用进程PID为1375

# Mac/Linux环境
```sh
# 查看端口4000的占用情况
sudo lsof -i :4000

# 根据占用的PID来结束进程
sudo kill -9 1375
```

# Windows环境
```sh
netstat -aon|findstr "4000"
```

结束进程
1.使用命令
```sh
taskkill /T /F /PID 1375
```
2.使用任务管理器来结束进程
