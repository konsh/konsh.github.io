---
title: 引用JSEncrypt模块提示 ReferenceError： window is not defined。解决方案
date: 2024-04-26 17:08:35
tags: 
    - JSEncrypt
    - Pycharm
    - 爬虫
    - JS逆向
category: 开发
keywords: JS逆向, 爬虫, Python
description: 引用JSEncrypt模块报错提示 ReferenceError： window is not defined
cover: /img/jsencrypto-error.png
---

在使用jsencrypto时，在Pycharm中执行代码提示`window is not defined`。
![jsencrypto error message](/img/jsencrypto-error.png)
问题原因：在IDE中是没有Window对象的，所以在执行代码的过程中会出现找不到对象的异常报错。

网上找了下解决方案，记录一下：
## 方案一：
    问了下chatgpt，chatgpt建议我安装使用一个叫jsdom的包。在JS文件中使用jsdom来模拟Window对象。ok，来试试。
    
    ```sh
    npm install jsdom
    ```
    在JS文件引用它
    ```javascript
    const jsdom = require('jsdom');
    const { JSDOM } = jsdom;

    // 创建一个模拟的 window 对象
    const { window } = new JSDOM();

    // 设置全局的 window 对象
    global.window = window;

    // 在这里写下您的 JavaScript 代码，可以使用 window 对象了
    // ...
    ```
    执行后错误依旧，看了下我的报错位置，是在jsencrypto包的内部报错而不是在我创建的JS文件里。那么这个方案也就pass。

## 方案二
    在源码中添加`window = this;`，这里有两种添加方式，①是在包的源文件中添加；②是在我的JS代码引用jsencrypto之前加上这句。
    因为我的程序后续还要部署到服务器上，所以①这个方案不就考虑了。那么直接试试②
    ```javascript
    window = this;
    const jsencrypt = require('jsencrypt') 

    ```


