npm(1) -- JavaScript 包管理器
====================================

## 概述

    npm <command> [args]

## 版本

@VERSION@

## 描述

npm 是 Node 平台的 JavaScript 包管理器。它将模块放在适当的位置，这样 Node
可以找到它们，并且明智地管理依赖冲突。

它高度可配置，支持各种用例。通常，它被用于发布、发现、安装、开发 Node 程序。

运行 `npm help` 来获取可用命令列表。

## 重要信息

npm 默认被配置为使用 npm 股份有限公司的公共 registry https://registry.npmjs.org 。该 npm 公共 registry 的使用服从于 https://www.npmjs.com/policies/terms 上的使用条款。

你可以配置 npm，使用任何你喜欢的兼容的 registry，甚至运行你自己的 registry。
其他人的 registry 使用受他们的使用条款约束。

## 介绍

你用 npm 可能因为你想要安装东西。

使用 `npm install blerg` 来安装最新版的 "blerg"。更多信息查看 `npm-install(1)`。
它可以做很多事。

使用 `npm search` 命令来显示所有可用的内容。

使用 `npm ls` 来显示所有你已经安装的内容。

## 依赖

如果一个包通过 git URL 引用另外一个包，npm 需要依赖预先安装的 git。

如果 npm 尝试安装的其中一个包，是一个原生 Node 模块，并且需要编译 C++ 代码，npm 将使用 
[node-gyp](https://github.com/nodejs/node-gyp) 完成这项工作。

对于 Unix 系统，node-gyp 需要 Python、make 和一个 buildchain，如 GCC。在 Windows
上，需要 Python 和 Microsoft Visual Studio C++。node-gyp 不支持 Python 3。
更多信息访问 [node-gyp 代码仓库](https://github.com/nodejs/node-gyp)
和 [node-gyp Wiki](https://github.com/nodejs/node-gyp/wiki)。

## 目录

See `npm-folders(5)` to learn about where npm puts stuff.

In particular, npm has two modes of operation:

* global mode:
  npm installs packages into the install prefix at
  `prefix/lib/node_modules` and bins are installed in `prefix/bin`.
* local mode:
  npm installs packages into the current project directory, which
  defaults to the current working directory.  Packages are installed to
  `./node_modules`, and bins are installed to `./node_modules/.bin`.

Local mode is the default.  Use `-g` or `--global` on any command to
operate in global mode instead.

## 开发者用法

If you're using npm to develop and publish your code, check out the
following help topics:

* json:
  Make a package.json file.  See `package.json(5)`.
* link:
  For linking your current working code into Node's path, so that you
  don't have to reinstall every time you make a change.  Use
  `npm link` to do this.
* install:
  It's a good idea to install things if you don't need the symbolic link.
  Especially, installing other peoples code from the registry is done via
  `npm install`
* adduser:
  Create an account or log in.  Credentials are stored in the
  user config file.
* publish:
  Use the `npm publish` command to upload your code to the registry.

## 配置

npm is extremely configurable.  It reads its configuration options from
5 places.

* Command line switches:
  Set a config with `--key val`.  All keys take a value, even if they
  are booleans (the config parser doesn't know what the options are at
  the time of parsing).  If no value is provided, then the option is set
  to boolean `true`.
* Environment Variables:
  Set any config by prefixing the name in an environment variable with
  `npm_config_`.  For example, `export npm_config_key=val`.
* User Configs:
  The file at $HOME/.npmrc is an ini-formatted list of configs.  If
  present, it is parsed.  If the `userconfig` option is set in the cli
  or env, then that will be used instead.
* Global Configs:
  The file found at ../etc/npmrc (from the node executable, by default
  this resolves to /usr/local/etc/npmrc) will be parsed if it is found.
  If the `globalconfig` option is set in the cli, env, or user config,
  then that file is parsed instead.
* Defaults:
  npm's default configuration options are defined in
  lib/utils/config-defs.js.  These must not be changed.

See `npm-config(7)` for much much more information.

## 贡献

欢迎提交补丁！

如果你想要贡献，但不知道要做什么，请阅读贡献指导方针，并检查问题列表。

* [CONTRIBUTING.md](https://github.com/npm/cli/blob/latest/CONTRIBUTING.md)
* [Bug 追踪](https://npm.community/c/bugs)
* [Support 追踪](https://npm.community/c/support)

## BUGS

当你发现问题时，请报告它们：

* web:
  <https://npm.community/c/bugs>

一定要遵照模版和 bug 报告指导方针。如果你不确定它是 bug 或者遇到了详细的可复现的问题需要报告，
你也可以在 [支持论坛](https://npm.community/c/support) 上请求帮助。

## 作者

[Isaac Z. Schlueter](http://blog.izs.me/) ::
[isaacs](https://github.com/isaacs/) ::
[@izs](https://twitter.com/izs) ::
<i@izs.me>

## 参见

* npm-help(1)
* README
* package.json(5)
* npm-install(1)
* npm-config(1)
* npm-config(7)
* npmrc(5)
* npm-index(7)
