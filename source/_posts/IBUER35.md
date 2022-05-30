---
title: 使用boto3向AWS S3上传文件
date: 2022-05-07 15:23:57
tags:
    - AWS
    - Python
    - 上传文件
category: Python
keywords: AWS, 上传文件, boto3, Python
description: 使用AWS开发工具包boto3上传文件到S3上。
cover: https://cdn.jsdelivr.net/gh/konsh/CDN/img/IBUER35.jpeg
---

# 前言
Boto3是AWS官方提供的基于python3的开发工具包，Boto3 可以支持您轻松将 Python 应用程序、库或脚本与 AWS 服务进行集成，包括 Amazon S3、Amazon EC2 和 Amazon DynamoDB 等。

# 使用
## 安装
```sh
pip install boto3
```

## 初始化
```python
from boto3.session import Session

session = Session(aws_access_key_id=you_id, aws_secret_access_key=you_key)
s3_client = session.client('s3')
bucket_name = 'you_bucket'
```

## 上传本地文件
```python
file_path = "本地文件地址"
fname = "图片名称"
s3_client.upload_file(Filename=file_path, Bucket=bucket_name, key=fname)
```

## 上传二进制文件
在实际开发api接口实现文件上传功能时，无法使用上面的上传本地文件逻辑，原因是api接口中数据是以文件流的形式传递，所以需要采用二进制数据上传。以下是flask框架为例：
```python
from flask import request

_file = request.files.get('file')
s3_client.upload_fileobj(Fileobj=_file.stream, Bucket=bucket_name, Key=fname)
```