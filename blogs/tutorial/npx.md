---
title: npm 和 npx 的区别
date: 2022-04-27
author: huo
sidebar: 'auto'
tags:
- npm
- npx
categories:
- 教程
---


::: tip 介绍
npm：Node Package（包）Manager（管理器）
<br>
npx ：Node Package（包）Execute（执行）
:::
# npm 和 npx 的区别
## NPM

众所周知，npm 是 Node.js 的软件包管理器，其目标是自动化的依赖性和软件包管理。

这意味着，可以在 <font color=#0ABF5B>package.json</font> 文件中为项目指定所有依赖项（软件包），当需要为其安装依赖项时，只要运行 <font color=#0ABF5B>npm install</font> 即可。

它还提供了版本控制，即可以指定项目的依赖版本，这样可以在大多数情况下，防止更新破坏项目，或者使用首选版本。

## NPX
npx 是执行 Node.js 软件包的工具，它从 npm5.2 版本开始，就与 npm 捆绑在一起。

npx 执行时的查找顺序如下：

+ 默认情况下，首先检查路径中是否存在要执行的包（即在项目中）；
+ 如果存在，它将执行；
+ 若不存在，意味着尚未安装该软件包，npx 将安装其最新版本，然后执行它。

上述行为是 npx 的默认行为之一，但它具有可用来阻止的标志。

例如，如果运行 <font color=#0ABF5B>npx package-name --no-install</font>，意味着告诉 npx ，它应该仅执行 <font color=#0ABF5B>package-name</font>，如果之前未安装，则不安装。

## 示例

假设有一个名为 <font color=#0ABF5B>my-package</font> 的软件包，想要执行它。

如果没有 npx，要执行一个软件包，必须通过其本地路径运行来完成，如下所示：

```js
./node_modules/.bin/my-package
```

或在  <font color=#0ABF5B>package.json</font> 文件的 <font color=#0ABF5B>scripts</font> 中将其定义为单独的脚本，如下所示：

```js
{
  "name":"XXX",
  "version": "1.0.0",
  "scripts": {
    "my-package":"./node_modules/.bin/my-package"
  }
}
```

然后使用 <font color=#0ABF5B>npm run my-package</font> 运行。

现在，运用 npx，只需运行 <font color=#0ABF5B>npx my-package</font>，即可轻松实现此目的。