npm-explore(1) -- 浏览安装过的包
=============================================

## 概述

    npm explore <pkg> [ -- <command>]

## 描述

在指定的已安装的包目录下创建一个子 shell 。

如果指定了 command，它会在子 shell 中执行，然后立即终止。

这在 `node_modules` 文件夹中有 git 子模块的情况下特别有用。

```sh
npm explore some-dependency -- git pull origin master
```

注意，包不会自动向后重新构建，所以如果你做了任何更改一定要使用 `npm rebuild <pkg>`。

## 配置

### shell

* 默认值: SHELL 环境变量，或者 POSIX 系统上的 "bash"，或者 Windows 上的 "cmd"
* 类型: path

运行 `npm explore` 命令的 shell。

## 参见

* npm-folders(5)
* npm-edit(1)
* npm-rebuild(1)
* npm-build(1)
* npm-install(1)
