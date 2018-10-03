npm-repo(1) -- 在浏览器中打开包的代码仓库页面
========================================================

## 概述

    npm repo [<pkg>]

## 描述

本命令尝试猜测包的代码仓库 URL 地址，然后尝试使用 `--browser` 配置参数打开。
如果没有提供包名，它会在当前文件夹中搜索 `package.json`，使用 `name` 属性。

## 配置

### browser

* 默认值: OS X: `"open"`, Windows: `"start"`, 其他系统: `"xdg-open"`
* 类型: 字符串

浏览器，被 `npm repo` 命令调用，用于打开网站。

## 参见

* npm-docs(1)
* npm-config(1)
