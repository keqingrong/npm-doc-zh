npm-repo(1) -- 在浏览器中打开包的仓库页面
========================================================

## 概述

    npm repo [<pkg>]

## 描述

This command tries to guess at the likely location of a package's
repository URL, and then tries to open it using the `--browser`
config param. If no package name is provided, it will search for
a `package.json` in the current folder and use the `name` property.

## 配置

### browser

* 默认值: OS X: `"open"`, Windows: `"start"`, 其他系统: `"xdg-open"`
* 类型: 字符串

浏览器，被 `npm repo` 命令调用，用于打开网站。

## 参见

* npm-docs(1)
* npm-config(1)
