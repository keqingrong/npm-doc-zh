npm-start(1) -- 启动包
===============================

## 概述

    npm start [-- <args>]

## 描述

运行包的 `"scripts"` 对象的 `"start"` 属性中指定的任意命令。如果 `"scripts"`
对象没有指定 `"start"` 属性，它将会运行 `node server.js`。

从 [`npm@2.0.0`](https://blog.npmjs.org/post/98131109725/npm-2-0-0) 起，
执行脚本时，你可以使用自定义参数。更多细节参考 `npm-run-script(1)`。

## 参见

* npm-run-script(1)
* npm-scripts(7)
* npm-test(1)
* npm-restart(1)
* npm-stop(1)
