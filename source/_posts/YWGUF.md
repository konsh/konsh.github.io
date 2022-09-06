---
title: Fastapi中使用异步非阻塞
date: 2022-09-06 11:37:23
category: 开发
tags: [Python]
keywords: Python, Fastapi, 异步非阻塞, 线程
description: fastapi中使用异步非阻塞
cover: https://cdn.jsdelivr.net/gh/konsh/CDN/img/logo-fastapi.png
---
原项目前后端不分离，拆分重构为前后端分离。原来的后端框架用的是flask，多重考虑之下选择了Fastapi这个异步框架。然后在重构过程中发现了一个比较尴尬的问题，flask下在一些接口中使用了线程去处理入库数据。

同时还有鉴于8月的新规（《互联网用户账号信息管理规定》），结合业务需求，需要记录并显示用户的IP归属地。没办法，只能研究了下Fastapi中异步非阻塞的实现方法。

以获取用户IP归属地为例

## 关键代码
```python
# -*- coding: utf-8 -*-
import threading

import asyncio
from fastapi import FastAPI
from starlette.requests import Request


app = FastAPI()

# 创建一个专门处理事件循环的函数
def start_loop(loop):
    asyncio.set_event_loop(loop)
    loop.run_forever()

# 获取请求IP
def get_client_ip(request: Request):
    headers = dict(request.headers)
    ip = headers.get('x-forwarded-for', '')
    return ip    

# 获取请求IP归属地，根据自身需求选择免费还是付费的接口调用，得到IP归属地后更新DB表
async def update_user_ip_area(ip, userId):
    pass


@app.post('/test')
async def test_api(*, req: Request):
    ip = get_client_ip(req)
    coroutine1 = update_user_ip_area(ip, userId)
    new_loop = asyncio.new_event_loop()
    t = threading.Thread(target=start_loop, args=(new_loop,))
    t.start()
    _run = asyncio.run_coroutine_threadsafe(coroutine1, new_loop)
    return {'code': 1, 'msg': 'success'}
```

## 优化
- 需要注意Fastapi的接口是靠协程来完成的，如果在部署的时候分配给程序的资源不够，就很容易造成资源堵塞，特别是在并发的场景下。
- 选择用户比较关键且触发请求较少的接口来完成该功能。
- 若是需要在请求比较频繁的接口中使用，可以对IP进行缓存，当IP不同时再触发该逻辑，这样也可以减少IP归属地接口的请求。

