---
title: Python连接Redis集群的方法
date: 2022-05-07 15:23:28
tags: 
    - Databas
    - Redis
    - 中间件
    - Python
category: Python
keywords: Database, Redis, 中间件, Python
description: Python连接Redis集群的方式
cover: https://cdn.jsdelivr.net/gh/konsh/CDN/img/ESFS7D.png
#cover: /img/ESFS7D.png
---

版本说明：
- python 3.8
- redis 3.5.3
- redis-py-cluster 2.1.3

# 连接主从/哨兵模式

安装依赖
```sh
pip install redis==3.5.3
```

python示例
```python
import redis

conn_pool = redis.ConnectionPool(host=HOST, port=PORT, password=AUTH, db=db)
client = redis.Redis(connection_pool=conn_pool)
```

# 连接Cluster集群模式
安装依赖
```sh
pip install redis-py-cluster==2.1.3
```

python示例
```python
from rediscluster import RedisCluster

client = RedisCluster(startup_nodes=[{'host': HOST, 'port': PORT}], password=AUTH, decode_responses=True, skip_full_coverage_check=True) # 若是连接不成功，则追加参数ssl=True
```
