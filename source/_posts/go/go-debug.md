---
title: Golang Debug 的正确使用姿势
post_meta:
  post:
    date_type: both
    date_format: relative
    categories: true
    tags: true
    label: true
copyright_author: Starboy
copyright_author_href: https://github.com/cris-w
copyright_info: 此文章版权归Starboy所有，如有转载，请注明来自原作者
date: 2024-12-30 23:17:55
tags: ['Golang', 'Debug', 'GoLand']
description: 介绍有关Golang debug的各种方式
categories: ['Golang']
cover: https://cdn.wujunhui.vip/blog/Golang.png
---

## 环境相关

{% note primary flat %}

要求本地正确安装Golang环境（建议直接使用GoLand安装最新sdk）！！！



Golang 版本：1.23.4 (推荐1.18及以上)

GoLand 版本：2024.3.1

{% endnote %}

## 本地调试

本地调试就直接在本地通过`debug`模式执行`main`函数，并在希望停止的地方添加断点。（具体操作不在赘述，不会本地调试建议在b占搜索相关视频学习）

## 附加到进程

附加到进程就是在给本地一个正在运行的go进程添加断点调试。

#### 步骤1. 安装 gops 包

```shell
go install github.com/google/gops@latest
```

安装后检查在本地`${GOPATH}/bin`目录下是否存在`gops`，存在即安装成功

#### 步骤2. 构建并运行程序

```shell
# 构建
go build -gcflags="all=-N -l" -o <appName>

# 运行
./<appName>
```

#### 步骤3. 附加并调试正在运行的进程

点击功能菜单 `Run -> Attach to Process...`，在弹出窗口选择当前正在运行的go进程即可进行调试，具体调试操作同本地调试。

## 远程调试

{% note danger flat %}
远程调试要求远程计算机与本地具有相同的go环境以及代码，并且暴露调试端口如`2345`
{% endnote %}

#### 步骤1. 远程计算机安装 Delve 包

```shell
go install github.com/go-delve/delve/cmd/dlv@latest
```

安装后检查在本地`${GOPATH}/bin`目录下是否存在`dlv`，存在即安装成功

#### 步骤2. 远程计算机构建并运行程序

```shell
# 构建
go build -gcflags="all=-N -l" -o <appName>

# 运行
# 方案一
dlv --listen=:2345 --headless=true --api-version=2 exec ./<appName>

# 方案二
# 运行程序
./<appName>
# 获取进程号 <PID>
ps -ef | grep <appName>
# 运行 delve
dlv --listen=:2345 --headless=true --api-version=2 attach <PID>
```

#### 步骤3. 本地计算机上创建 Go Remote 运行/调试配置﻿

1. 点击编辑 | 运行配置。或者，单击工具栏上的运行/调试配置列表并选择`Edit Configurations`。
2. 在Run/Debug Configurations对话框中，单击Add按钮 `+` 并选择`Go Remote`。
3. 在主机字段中，输入主机 IP 地址（例如`192.168.1.33`）。
4. 在端口字段中，键入您在步骤 2中配置的调试器端口（例如，`2345`）。
5. 单击确定。
6. 具体调试过程同本地调试。



{% note info flat %}
本文简要介绍有关调试的核心操作，更详细的介绍可以参考[此处](https://www.javatiku.cn/goland/2609.html)
{% endnote %}
