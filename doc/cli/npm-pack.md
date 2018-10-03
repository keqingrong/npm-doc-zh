npm-pack(1) -- 创建包的 tarball 文件
==============================================

## 概述

    npm pack [[<@scope>/]<pkg>...] [--dry-run]

## 描述

任何可安装的，包括包文件夹、tarball、tarball url、名称@标签（name@tag）、
名称@版本（name@version）、名称，或者限定范围的名称（scoped name），
本命令将会获取它保存到缓存中，然后将这个 tarball 复制到当前工作目录，保存为
`<name>-<version>.tgz` 形式，最后将文件名写到标准输出。

如果同一个包被指定了多次，后一次的将会覆盖前一次的文件。

如果没有提供参数，npm 会打包当前文件夹。

`--dry-run` 参数将会做一切打包的时候做的事情，除了真正地打包。它会报告哪些东西会被打包到
tarball 文件中。

## 参见

* npm-cache(1)
* npm-publish(1)
* npm-config(1)
* npm-config(7)
* npmrc(5)
