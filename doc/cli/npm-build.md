npm-build(1) -- 构建包
===============================

## 概述

    npm build [<package-folder>]

* `<package-folder>`:
  根目录包含 `package.json` 文件的文件夹。

## 描述

本命令是被 `npm link` 和 `npm install` 调用的管道命令（plumbing command）。

它通常应该在安装过程中被调用，但如果你需要直接运行它，请运行：

```sh
npm run-script build
```

## 参见

* npm-install(1)
* npm-link(1)
* npm-scripts(7)
* package.json(5)
