---
title: Vuepress+vercel搭建个人博客
date: 2022-03-20
author: huo
sidebar: 'auto'
sticky:
- description
tags:
- vuepress
- 教程
categories:
- 教程
---

::: tip 介绍
服务器和域名利用vercel的免费资源，博客框架采用vuepress,主题采用 vuepress-theme-reco@1.6.1
:::

# 博客搭建
首先我们需要把博客初始化

## 安装

```bash
npx @vuepress-reco/theme-cli init

# or

npm install @vuepress-reco/theme-cli -g
theme-cli init

# or 

yarn global add @vuepress-reco/theme-cli
theme-cli init

```

## github
如果没有github账号，可以自行注册一个。

<b>连接github仓库</b>

首先我们创建一个github仓库(过程略)。

然后在本地初始化git

```bash
git init
git add .
git commit -m 'init'
```

然后连接远程仓库。
```bash
git remote add origin 你的github仓库地址
git branch -M main
git push -u origin main
```

## 部署博客
我们利用的是vercel的免费资源，所以我们需要先注册个[vercel](https://vercel.com/dashboard)账号
登录之后进入 [vercel](https://vercel.com/dashboard)页面

![Image text](https://www.sharesomething.cn/course/vercel.jpg)
点击New Project按钮导入刚刚创建的github仓库

导入之后全部选择默认配置，博客会自己构建，以后每次本地push之后，vercel会自动构建



## 更换域名
如果你不想用他的域名的话，可以进入你创建的项目，进入settings>>domains添加自己的域名
::: tip 介绍
如果有什么疑问，可以在评论区提出。 关注人数较多的话，会考虑出更加详细的教程  [b站视频链接](https://www.bilibili.com/video/BV17Q4y1Y7LF?spm_id_from=333.999.0.0)
:::