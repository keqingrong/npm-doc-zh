npm-rebuild(1) -- 重新构建包
===================================

## 概述

    npm rebuild [[<@scope>/<name>]...]

    别名: npm rb

## 描述

本命令会在匹配到的文件夹中运行 `npm build`。当你安装一个新版本 Node，
并且必须使用新的二进制文件重新编译所有的 C++ 插件时，它会很有帮助。

## 参见

* npm-build(1)
* npm-install(1)
