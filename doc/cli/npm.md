npm(1) -- JavaScript 包管理器
====================================

## 概述

    npm <command> [args]

## 版本

@VERSION@

## 描述

npm 是 Node 平台的 JavaScript 包管理器。它将模块放在适当的位置，这样 Node
可以找到它们，并且智能地管理依赖冲突。

它高度可配置，支持各种用例。通常，它被用于发布、发现、安装、开发 Node 程序。

运行 `npm help` 来获取可用命令列表。

## 重要信息

npm 默认被配置为使用 npm 股份有限公司的公共 registry https://registry.npmjs.org 。
该 npm 公共 registry 的使用服从于 https://www.npmjs.com/policies/terms 上的使用条款。

你可以配置 npm 使用任何你喜欢的兼容的 registry，甚至运行你自己的 registry。其他人的
registry 的使用受他们的使用条款约束。

## 介绍

你用 npm 可能因为你想要安装东西。

使用 `npm install blerg` 来安装最新版的 `"blerg"`。更多信息查看 `npm-install(1)`。
它可以做很多事。

使用 `npm search` 命令来显示所有可用的内容。

使用 `npm ls` 来显示所有你已经安装的内容。

## 依赖

如果一个包通过 git URL 引用另外一个包，npm 需要依赖预先安装的 git。

如果 npm 尝试安装的其中一个包，是一个原生 Node 模块，并且需要编译 C++ 代码，npm 将使用 
[node-gyp](https://github.com/nodejs/node-gyp) 完成这项工作。对于 Unix 系统，
node-gyp 需要 Python、make 和一个构建工具链，如 GCC。在 Windows 上，需要 Python 和
Microsoft Visual Studio C++。node-gyp 不支持 Python 3。
更多信息访问 [node-gyp 代码仓库](https://github.com/nodejs/node-gyp)
和 [node-gyp Wiki](https://github.com/nodejs/node-gyp/wiki)。

## 目录

查看 `npm-folders(5)` 来了解 npm 将东西放在哪儿。

特别地，npm 有两种操作模式：

* 全局模式：
  npm 将包安装到目录前缀 `prefix/lib/node_modules`
  中，二进制文件安装到 `prefix/bin` 中。
* 局部模式：
  npm 将包安装到当前项目目录（默认为当前工作目录）。所有的包被安装到 `./node_modules`，
  二进制文件被安装到 `./node_modules/.bin`。

局部模式是默认模式。在任意命令上使用 `-g` 或者 `--global` 改为全局模式操作。

## 开发者用法

如果你正在使用 npm 来开发并且发布你的代码，检查以下的帮助主题：

* json:
  创建 `package.json` 文件。见 `package.json(5)`。
* link:
  将你当前工作的代码链接到 Node 的 path 路径，以便每次变更时不需要重新安装。
  使用 `npm link` 来实现。
* install:
  如果你不需要符号链接的话，它是安装东西的好主意。尤其是通过 `npm install`
  从 registry 安装其他人的代码。
* adduser:
  创建账号或者登录。证书会被存储到用户配置文件中。
* publish:
  使用 `npm publish` 命令上传你的代码到 registry 。

## 配置

npm 高度可配置。他会从 5 个地方读取它的配置项。

* 命令行开关：
  通过 `--key val` 设置配置。所有的 key 都有一个 value，即使它们是布尔值
  （配置解析器在解析时不知道选项是什么）。如果没有提供 value，那么选项会被设置为布尔值 `true`。
* 环境变量：
  在环境变量中通过设置带 `npm_config_` 前缀名称的配置。如：`export npm_config_key=val`。
* 用户配置：
  该文件位于 `$HOME/.npmrc`，是一组 INI 格式的配置。如果存在，它会被解析。
  如果在命令行或者环境变量中设置了 `userconfig` 选项，将会使用它代替。
* 全局配置：
  如果可以找到 `../etc/npmrc`（从 Node 可执行文件处，默认会解析到
  `/usr/local/etc/npmrc`）文件，它将会被解析。
* 默认值：
  npm 的默认配置项定义在 `lib/utils/config-defs.js` 中。这些必须是不可更改的。

更多信息参见 `npm-config(7)`。

## 贡献

欢迎提交补丁！

如果你想要贡献，但不知道要做什么，请阅读贡献指导方针，并检查问题列表。

* [CONTRIBUTING.md](https://github.com/npm/cli/blob/latest/CONTRIBUTING.md)
* [Bug 追踪](https://npm.community/c/bugs)
* [Support 追踪](https://npm.community/c/support)

## 缺陷

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
