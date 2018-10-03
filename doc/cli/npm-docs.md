npm-docs(1) -- 在 Web 浏览器中打开包的文档页面
========================================================

## 概述

    npm docs [<pkgname> [<pkgname> ...]]
    npm docs .
    npm home [<pkgname> [<pkgname> ...]]
    npm home .

## 描述

本命令尝试猜测包的文档页面 URL 地址，然后尝试使用 `--browser` 配置参数打开。
你可以一次传多个包名。如果没有提供包名，它会在当前文件夹中搜索 `package.json`，使用 `name`
属性。

## 配置

### browser

* 默认值: OS X: `"open"`, Windows: `"start"`, 其他系统: `"xdg-open"`
* 类型: 字符串

浏览器，被 `npm docs` 命令调用，用于打开网站。

### registry

* 默认值: `https://registry.npmjs.org/`
* 类型: url

npm 包 registry 的基础 URL。

## 参见

* npm-view(1)
* npm-publish(1)
* npm-registry(7)
* npm-config(1)
* npm-config(7)
* npmrc(5)
* package.json(5)
