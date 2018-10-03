npm-help-search(1) -- 搜索 npm 帮助文档
===================================================

## 概述

    npm help-search <text>

## 描述

本命令会搜索 npm markdown 文档文件，查找提供的术语，然后列出结果，按相关性排序。

如果仅找到了一个结果，那么会显示结果的帮助主题。

如果传给 `npm help` 的参数不是已知的帮助主题，它将会调用 `help-search`。
几乎没有必要直接调用本命令。

## 配置

### long

* 类型: 布尔值
* 默认值: false

如果为 true，"long" 标记将会使 help-search 输出文档中术语找到之处的上下文。

如果为 false，help-search 将只会列出找到的帮助主题。

## 参见

* npm(1)
* npm-help(1)
