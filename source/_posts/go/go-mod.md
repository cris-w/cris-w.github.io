---
title: go mod 依赖管理
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
date: 2024-12-31 16:44:15
tags: ['Golang', '依赖管理']
description: Golang的依赖管理相关
comments: true
categories: ['Golang']
cover: https://cdn.wujunhui.vip/blog/Golang.png
---
{% note primary flat %}
本文介绍Golang的依赖管理相关，包括go.mod文件中各函数的作用，go mod常用指令和依赖管理相关指令
{% endnote %}
## go mod 文件介绍

```go
// 模块名
module go_server
// go sdk 版本
go 1.23.4

// 当前module(项目)依赖的包
require (
	// dependency latest
)

// 排除的第三方包
exclude (
	// dependency latest
)

// 修改依赖包路径或版本 (依赖包发生迁移/原始包无法访问/使用本地包替换原始包)
replace (
	// source latest => target latest
)

// 撤回 (当前项目作为其他项目的依赖，如果某个版本出现了问题则可以使用该命令撤回该版本)
retract (
	// v1.0.0
	// v1.0.2
)
```

## go mod 命令

```shell
# 将模块下载到本地缓存，需要指定模块路径及版本号
go mod download
# 例如
go mod download github.com/gin-gonic/gin@v1.9.0

# 初始化模块到到当前目录
go mod init
# 例如
go mod init myApp

# 添加缺少依赖，删除未使用依赖 (常用！)
go mod tidy

# 通过工具或脚本编辑go.mod
go mod edit
# 例如
go mod edit -require="github.com/gin-gonic/gin v1.10.0"

# 根据go.mod中的依赖制作vendor副本，有了vendor本地项目不再依赖本地缓存
go mod vendor

# 验证依赖是否正确
go mod verify

# 返回对指定模块依赖关系的最短路径，解释为什么依赖指定包
go mod why
# 例如
go mod why github.com/go-playground/validator/v10
```



## go install/get/clean

```shell
# go install 安装可执行插件
# 例如
go install github.com/go-delve/delve/cmd/dlv@latest

# go get 获取模块信息并更新 go.mod，若本地缓存没有该模块，则下载，反正直接引用
# 例如
go get github.com/gin-gonic/gin@1.9.0

# go get -u 更新依赖模块，并更新mo.mod

# go clean 清理临时目录中的文件
# 例如清除整个module下载的缓存文件
go clean -modcache
```

