npm-prefix(1) -- 显示目录前缀
===============================

## 概述

    npm prefix [-g]

## 描述

打印当前目录前缀到标准输出。如果不指定 `-g` 参数，则为最近的包含 `package.json`
文件的父级目录。

如果指定了 `-g` 参数，将会是全局的前缀值。更多细节参考 `npm-config(7)`。

## 参见

* npm-root(1)
* npm-bin(1)
* npm-folders(5)
* npm-config(1)
* npm-config(7)
* npmrc(5)
