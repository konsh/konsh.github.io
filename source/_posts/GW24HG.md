---
title: Python爬虫练习-etree.HTML解析数据异常
date: 2023-11-21 17:26:40
tags: Python, lxml, xpath, 爬虫
---

这几天帮朋友写一个爬虫。可能因为太久没写爬虫了，总是遇到一些奇奇怪怪的问题，也可能是因为时间太久以至于忘了一些原理或者机制了。所以记录一下，防止以后遇到了又不知道是什么原因导致的。

## 描述
通过requests.get()方法获取到页面后，我使用了etree.HTML来解析该网页结构，再通过xpath提取出自己需要的内容。


核心代码：
```python
response = requests.get(url, headers=headers)
html_obj = etree.HTML(response.text)
comments = html_obj.xpath('//span[@class="XXX"]/text()')
```

## 问题出现
本以为数据可以正常获取，结果发现程序报错了，报错信息为```AttributeError: 'NoneType' object has no attribute 'xpath'```。

![程序报错信息](https://cdn.jsdelivr.net/gh/konsh/CDN/img/xpath异常报错信息.png)


## 解决
NoneType object has no attribute？试了下debug模式，发现在etree.HTML时没有获取到正确的Element对象，得到的是一个None

![pycharm debug定位](https://cdn.jsdelivr.net/gh/konsh/CDN/img/pycharm_debug问题定位_xpath.png)

OK。问题已经找到了，那么原因是什么呢？看下源码

![HTML方法源码说明](https://cdn.jsdelivr.net/gh/konsh/CDN/img/HTML方法源码说明.png)

呃......好吧，换个思路。response中的text是Unicode编码，看了下页面，原来在页面中指定了编码UTF-8。

破案了，在lxml中是不支持解析带有coding声明的字符串，那么该怎么处理呢？

在response中有一个content，与text不同的是content是byte类型，那么就换成它来试试看吧
![lxml解析成功](https://cdn.jsdelivr.net/gh/konsh/CDN/img/HTML解析成功.png)
