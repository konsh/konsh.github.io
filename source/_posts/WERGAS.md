---
title: 免费常用IP归属地查询接口
date: 2022-07-29 15:30:03
tags: [工具, Python, 中间件]
category: 开发
keywords: IP, IP归属地, 免费
description: 免费常用的IP归属地接口
cover: https://cdn.jsdelivr.net/gh/konsh/CDN/img/ipaddress.webp
---

# IP-API接口
文档： http://ip.taobao.com/instructions

请求示例：

```python
api_url = 'http://ip.taobao.com/outGetIpInfo?ip=218.18.45.7&accessKey=alibaba-inc'
result = requests.get(api_url)
res_json = result.json()

res_json:
{
    data: {
        area: "",
        country: "中国",
        isp_id: "100017",
        queryIp: "218.18.45.7",
        city: "深圳",
        ip: "218.18.45.7",
        isp: "电信",
        county: "",
        region_id: "440000",
        area_id: "",
        county_id: null,
        region: "广东",
        country_id: "CN",
        city_id: "440300"
    },
    msg: "query success",
    code: 0
}
```

# IP-API接口
文档： https://ip-api.com/docs/api:json

请求示例：
```python
api_url = 'http://ip-api.com/json/218.18.45.7?lang=zh-CN'
result = requests.get(api_url)
res_json = result.json()

res_json:
{
    status: "success",
    country: "中国",
    countryCode: "CN",
    region: "GD",
    regionName: "广东",
    city: "深圳",
    zip: "",
    lat: 22.5559,
    lon: 114.0577,
    timezone: "Asia/Shanghai",
    isp: "CHINANET Guangdong province Shenzhen MAN network",
    org: "Chinanet GD",
    as: "AS134774 CHINANET Guangdong province Shenzhen MAN network",
    query: "218.18.45.7"
}
```

# 太平洋IP
文档：http://whois.pconline.com.cn/

请求示例：
```python
api_url = 'http://whois.pconline.com.cn/ipJson.jsp?ip=218.18.45.7&json=true'
result = requests.get(api_url)
res_json = result.json()

res_json:
{
    "ip":"218.18.45.7",
    "pro":"广东省",
    "proCode":"440000",
    "city":"深圳市",
    "cityCode":"440300",
    "region":"南山区",
    "regionCode":"440305",
    "addr":"广东省深圳市南山区 电信ADSL",
    "regionNames":"",
    "err":""
}
```

# useragentinfo
文档： https://ip.useragentinfo.com/

请求示例：
```python
api_url = 'https://ip.useragentinfo.com/json?ip=218.18.45.7'
result = requests.get(api_url)
res_json = result.json()

res_json:
{
    "country":"中国",
    "short_name":"CN",
    "province":"广东省",
    "city":"深圳市",
    "area":"南山区",
    "isp":"电信",
    "net":"",
    "ip":"218.18.45.7",
    "code":200,
    "desc":"success"
}
```

# 说在最后
免费接口学习使用就好，至于业务需求，俗话说得好：能用钱解决的问题都不加问题~