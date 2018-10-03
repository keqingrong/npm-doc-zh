npm-help(1) -- 获取 npm 帮助
==============================

## 概述

    npm help <term> [<terms..>]

## 描述

如果提供了主题，将会显示合适的文档页。

如果主题不存在，或者提供了多个术语（term ），那么会运行 `help-search` 命令寻找一个匹配项。
注意，如果 `help-search` 找到单个主题，它将会对那个主题运行 `help`，
所以唯一匹配等同于指定一个主题名。

## 配置

### viewer

* 默认值: POSIX 系统上的 "man"，Windows 上的 "browser"
* 类型: path

该程序用于查看帮助内容。

设置为 `"browser"` 会在默认的 Web 浏览器中查看 HTML 帮助内容。

## 参见

* npm(1)
* README
* npm-folders(5)
* npm-config(1)
* npm-config(7)
* npmrc(5)
* package.json(5)
* npm-help-search(1)
* npm-index(7)
