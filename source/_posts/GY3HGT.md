---
title: hexo操作
date: 2021-06-24 16:04:49
category: hexo
tags: [hexo, 建站]
keywords: hexo, 建站
description: 常用hexo命令操作
cover: https://cdn.jsdelivr.net/gh/konsh/CDN/img/GY3HGT.png
---

# 前提
该文章仅作为记录常用的hexo使用命令，若需从头开始建站请访问[hexo官网文档](https://hexo.io/zh-cn/docs/)

# 操作命令
## 新建
```sh
hexo new [layout] <title>
```
参数说明

参数 | 描述
:-:|:-:
-p, --path | 自定义新文章路径
-r, --relpace | 替换同名文章
-s, --slug | 文章slug，作为新文章的文件名和发布后的URL

## 生成静态文件
```sh
hexo generate

# 可简写为
hexo g  
```
参数说明

参数 | 描述
:-:|:-:
-d, --deploy | 文件生成后立即部署网站
-w, --watch | 监视文件变动
-b, --bail | 生成过程中若发生任何未处理的异常则抛出异常
-f, --force | 强制重新生成文件<br>Hexo引入了差分机制，若public目录存在，那么hexo g 只会重新生成改动的文件<br>使用该参数的效果相当于 hexo clean && hexo generate
-c, --concurrency | 最大同时生成文件的数量，默认无限制

## 发表草稿
```sh
hexo publish [layout] <filename>
```

## 启动服务
```sh
hexo server

# 可简写为
hexo s
```
参数说明

参数 | 描述
:-:|:-:
-p, --port | 重设端口
-s, --static | 只使用静态文件
-l, --log | 启动日志记录，使用覆盖记录格式

## 部署网站
```sh
hexo deploy

# 可简写为
hexo d
```
参数说明

参数 | 描述
:-:|:-:
-g, --generate | 部署之前预先生成静态文件

## 清除缓存和静态资源
```sh
hexo clean
```
清除缓存文件（db.json）和已生成的静态文件（public）

在某些情况下（特别是更换主题），使用该命令可解决主题不生效问题
