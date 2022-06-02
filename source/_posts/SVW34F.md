---
title: Golang自动导包配置
date: 2022-05-11 14:43:50
tags:
- vs code
- Golang
- Goland
category: Golang
keywords: Golang, Goland, vs code
description: golang在IDE中自动导包配置
cover: https://cdn.jsdelivr.net/gh/konsh/CDN/img/SVW34F.png
---

# 前言

Go开发者所使用的IDE中无非vs code和Goland两种。近期有golang的开发需求，所以找了下关于golang的相关使用及配置。

以下仅限对代码编辑器的配置，golang的安装还有环境配置不在本次探讨中。

# vscode中配置golang
vs code是一款由微软开发的跨平台的免费编辑器。该软件支持语法高亮、代码自动补全、代码重构功能，并且内置了命令行工具和Git版本控制系统。

## 安装go插件和工具包
### 扩展工具中安装GO插件

![vscode安装Go插件](https://cdn.jsdelivr.net/gh/konsh/CDN/img/vscode-go插件.png)

### 安装GO工具包
打开控制面板输入```go:install/update tools```，勾选全部插件进行安装。
 > 打开控制面板的方法
    >
    >> 1. 查看 - 命令面板
    >>
    >> 2. mac系统可使用快捷键command+shift+P
    >>
    >> 3. win系统可使用快捷键ctrl+shift+P

![vscode-go工具包安装1](https://cdn.jsdelivr.net/gh/konsh/CDN/img/vscode-go工具包安装1.png)

![vscode-go工具包安装2](https://cdn.jsdelivr.net/gh/konsh/CDN/img/vscode-go工具包安装2.png)

### 更新配置文件
在 Preferences/首选项 -> Setting/设置 然后输入 go，然后选择 setting.json，填入你想要修改的配置
```
    "go.autocompleteUnimportedPackages": true,
    "gopls": {
        "experimentalWorkspaceModule": true
    },
    "go.inferGopath": true,
    "go.toolsManagement.autoUpdate": true,
    "go.gotoSymbol.includeImports": true,
    "go.useCodeSnippetsOnFunctionSuggest": true,
    "go.useCodeSnippetsOnFunctionSuggestWithoutType": true,
```

# Goland中配置golang

Preferences -> Go -> Go Modules配置参数
![Goland setting](https://cdn.jsdelivr.net/gh/konsh/CDN/img/goland-1.png)