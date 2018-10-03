npm-restart(1) -- 重新启动包
===================================

## 概述

    npm restart [-- <args>]

## 描述

本命令重新启动一个包。

本命令运行包的 `"stop"`、`"restart"`、`"start"` 脚本，以及相关的 `pre-` 和 `post-`
脚本，按照以下给的顺序：

1. prerestart
2. prestop
3. stop
4. poststop
5. restart
6. prestart
7. start
8. poststart
9. postrestart

## 注意

注意，除了 `"stop"` 和 `"start"` 脚本之外，还会运行 `"restart"` 脚本，但不会取代它们。

这是 `npm` 主版本 2.0 的行为。随着主版本号的增长，这种行为将会变化。

## 参见

* npm-run-script(1)
* npm-scripts(7)
* npm-test(1)
* npm-start(1)
* npm-stop(1)
* npm-restart(3)
