npm-init(1) -- 创建 package.json 文件
=======================================================

## 概述

    npm init [--force|-f|--yes|-y|--scope]
    npm init <@scope> (等同于 `npx <@scope>/create`)
    npm init [<@scope>/]<name> (等同于 `npx [<@scope>/]create-<name>`)

## 示例

使用 [`create-react-app`](https://npm.im/create-react-app) 创建一个基于 React
的新项目：

```sh
$ npm init react-app ./my-react-app
```

使用 [`create-esm`](https://npm.im/create-esm) 创建一个 ESM 兼容的新包：

```sh
$ mkdir my-esm-lib && cd my-esm-lib
$ npm init esm --yes
```

使用遗留的初始化命令生成一个简单的旧的 package.json 文件。

```sh
$ mkdir my-npm-pkg && cd my-npm-pkg
$ git init
$ npm init
```

生成文件时不询问问题：

```sh
$ npm init -y
```

## 描述

`npm init <initializer>` 可以被用于设置一个新的或者已存在的 npm 包。

在这种情况下，`initializer` 是一个命名为 `create-<initializer>` 的 npm 包，将会通过
[`npx(1)`](https://npm.im/npx) 安装，然后会执行它的执行文件——很可能会创建或者更新
`package.json`，并且执行其他初始化相关的操作。

该初始化命令可以被转换为相应的 `npx` 操作，如下所示：

* `npm init foo` -> `npx create-foo`
* `npm init @usr/foo` -> `npx @usr/create-foo`
* `npm init @usr` -> `npx @usr/create`

任何额外的选项都将会被直接传给该命令，所以 `npm init foo --hello` 将会被映射为
`npx create-foo --hello`。

如果省略了初始化器（只调用 `npm init`），init 将会回退到遗留的初始化行为。它将会问你一些问题，
然后写入 package.json 文件。它会尝试基于已存在的字段、依赖和选中的选项做出合理猜测。
它是严格附加的，所以会保留任何已经设置过的字段和值。你也完全可以使用 `-y`/`--yes` 跳过问卷调查。
如果你传了 `--scope`，它将会创建限定范围的包（scoped package）。

## 参见

* <https://github.com/npm/init-package-json>
* package.json(5)
* npm-version(1)
* npm-scope(7)
