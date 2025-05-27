---
title: hexo-start
date: 2025-05-27 19:18:07
description: hexo使用
tags: [blog]
categories: [博客]
post_meta:
  post:
    date_type: both # created or updated or both 文章页日期是创建日或者更新日或都显示
    date_format: relative # date/relative 显示日期还是相对日期
    categories: true # true or false 文章页是否显示分类
    tags: true # true or false 文章页是否显示标签
    label: true # true or false 显示描述性文字
copyright_author: Starboy
copyright_author_href: https://github.com/cris-w
copyright_info: 此文章版权归Starboy所有，如有转载，请注明来自原作者
---

### 本地搭建 hexo 静态博客

- 安装 hexo 框架: 打开 cmd 运行

```shell
$ npm install -g hexo-cli
```

- 新建一个文件夹，如 MyBlog ，进入该文件夹内，右击运行 git ，输入：

```shell
$ hexo init
```

- 生成完 hexo 模板，安装 npm ，运行：

```shell
$ npm install
```

没错，博客的主体部分到此已经完成了，来看看效果吧。运行：

```shell
$ hexo server
```

这时候打开浏览器，输入 `localhost:4000` 就可以看到博客目前的样子了。小小激动一下，然后按 `Ctrl + C` 就可以继续下面的操作了。



### 源文件备份

- 切记备份好本地的源文件，尤其是 Markdown 文件，其他配置一旦丢失则无法正常写博客，需要从头开始设置
- 建议使用 GitHub 同一个仓库备份
- 建议每当有一些改动就备份一次，或者每日备份一次
- 更多用法请查看 [Git 文档](https://git-scm.com/book/pl/v2/Appendix-C%3A-Git-Commands-Sharing-and-Updating-Projects)

```shell
# 添加前面设置好的博客仓库地址
git remote add https://github.com/your-name/your-name.github.io.git

# 添加并保存当前改动，并记录备注
git add .
git commit -m "源文件更新"

# 建立并切换到新的分支
git checkout -b source

# 将本地 source 分支的全部内容推送到远端仓库的 source 分支
git push origin source:source
```

### 用不同的电脑写博客

- 当在不同的电脑上写博客时，需要进行基础软件安装，再拉取远端备份 GitHub 的仓库到本地，进行博客的更新

- 下载安装 node.js （[官网下载安装](https://nodejs.org/en/)）
- 下载安装 git （[官网下载安装](https://git-scm.com/downloads)）
- 安装 hexo 框架: 打开 cmd 运行

```shell
npm install -g hexo-cli
```

- 进行本地更新

```shell
# 克隆仓库到本地
git clone https://github.com/your-name/your-name.github.io.git

# 如果本地已经克隆，每次更新博客前都需要拉取最新分支内容
git pull origin

# 切换到对应分支
git checkout source

# 下载butterfly主题 （如果你使用的是butterfly主题）
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly

# 安装 hexo 配置下的全部插件后可以开始更新编辑博客内容
npm install

# 修改内容后记得及时备份一条龙
git add .
git commit -m "博客更新xxx"
git push origin source:source

# 发布推送最新博客内容到域名站点
hexo clean
hexo g  # 生成静态文件
hexo s  # 本地预览博客效果
hexo d  # 发布最新博客内容
```

### 几个常用命令汇总

```shell
hexo g
#或 hexo generate，根据源文件生成静态网页
hexo d
#或 hexo deploy，发布推送到 GitHub Pages
hexo s
#或 hexo server，本地部署测试
hexo clean
# 清空静态网页 cache，然后 hexo d 重新生成
```


参考链接：https://www.philoli.com/building-a-blog-from-scratch/