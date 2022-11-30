---
title: Fastapi中使用后台任务
date: 2022-11-29 17:14:40
category: 开发
tags: [Python]
keywords: Python, Fastapi, 后台任务, 协程
description: Fastapi中使用后台任务
cover: https://cdn.jsdelivr.net/gh/konsh/CDN/img/logo-fastapi.png
---
之前在项目中使用是异步非阻塞方式处理线程任务，但是一段时间之后云服务监控提示出现异常，猜测应该是出现了资源阻塞。重新查看fastapi官方文档发现，fastapi其实提供了一个[BackgroundTasks](https://fastapi.tiangolo.com/tutorial/background-tasks/)的后台任务。

那么就记录一下吧~

```python
from fastapi import FastAPI, BackgroundTasks
from starlette.requests import Request


app = FastAPI()

# 获取请求IP
def get_client_ip(request: Request):
    headers = dict(request.headers)
    ip = headers.get('x-forwarded-for', '')
    return ip    

# 获取请求IP归属地，根据自身需求选择免费还是付费的接口调用，得到IP归属地后更新DB表
async def update_user_ip_area(ip, userId):
    pass


@app.post('/test')
async def test_api(*, req: Request, background_task: BackgroundTasks):
    ip = get_client_ip(req)
    background_task.add_task(update_user_ip_area, ip, userId)
    return {'code': 1, 'msg': 'success'}
```

## 注意点
- 在使用时必须在路径方法中导入并并定义一个参数，声明其类型为BackgroundTasks。
- 后台任务方法可以是`async def`函数，也可以是`def`函数，这并不影响函数的执行调用。
- 如果需要执行的是一个繁重的计算且可能需要多个进程运行（如不需要共享内存、变量等），使用其他更大的工具（Celery），他们的效果可能会更好。
- 它们往往需要更复杂的配置、消息/作业队列管理器（RabbitMQ或Redis），但她们允许在多个进程中运行后台任务，尤其是在多服务器中。
- 如果需要从同一个Fastapi应用程序访问变量和对象，或者需要执行小型后台任务，可以简单地使用BackgroundTasks。
