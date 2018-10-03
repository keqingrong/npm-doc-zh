npm-config(1) -- 管理 npm 配置文件
===================================================

## 概述

    npm config set <key> <value> [-g|--global]
    npm config get <key>
    npm config delete <key>
    npm config list [-l] [--json]
    npm config edit
    npm get <key>
    npm set <key> <value> [-g|--global]

    别名: c

## 描述

npm 会从命令行，环境变量，`npmrc` 文件，（某些情况下）`package.json` 文件获取配置设置。

关于 npmrc 文件的更多信息参见 `npmrc(5)`。

对有关机制更全面的讨论参见 `npm-config(7)`。

`npm config` 命令可以被用于更新、编辑用户和全局的 `npmrc` 文件内容。

## 子命令

`npm config` 支持以下子命令：

### set

    npm config set key value

将配置 `key` 设置为 `value`。

如果省略了 `value`，将会设置为 `"true"`。

### get

    npm config get key

输出配置值到标准输出。

### list

    npm config list

显示所有的配置设置。使用 `-l` 会显示所有的默认配置。使用 `--json` 会以 JSON 格式显示所有配置。

### delete

    npm config delete key

从所有的配置文件中删除 `key`。

### edit

    npm config edit

在编辑器中打开配置文件。使用 `--global` 标记来编辑全局配置。

## 参见

* npm-folders(5)
* npm-config(7)
* package.json(5)
* npmrc(5)
* npm(1)
