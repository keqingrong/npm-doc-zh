npm-deprecate(1) -- 将包的某个版本标记为已废弃
====================================================

## 概述

    npm deprecate <pkg>[@<version>] <message>

## 描述

本命令将会更新包的 npm registry 条目，向所有尝试安装它的人提供一个弃用的警告。

它适用于版本范围和指定版本，所以你可以像下面这样做：

```sh
npm deprecate my-thing@"< 0.2.3" "critical bug fixed in v0.2.3"
```

注意，你必须是包的所有者才能标记废弃。参见 `owner` 和 `adduser` 帮助主题。

要取消废弃一个包，为 `message` 参数指定一个空字符串（`""`）。

## 参见

* npm-publish(1)
* npm-registry(7)
