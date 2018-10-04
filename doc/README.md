npm(1) -- JavaScript 包管理器
==============================

[![构建状态](https://img.shields.io/travis/npm/cli/latest.svg)](https://travis-ci.org/npm/cli)

## 概述

这里有足够的信息能让你迅速上手。

一旦安装了 npm，可以通过 `npm help` 获取更多信息。

## 重要信息

**你需要 Node v6 或者更高的版本来运行该程序。**

要安装可以运行在 Node v5 和之前版本上的 **不支持的** 旧版 npm，请克隆该 git
仓库，查找旧的标签和分支。

npm 默认被配置为使用 npm 股份有限公司的公共 registry https://registry.npmjs.org 。
该 npm 公共 registry 的使用服从于 https://www.npmjs.com/policies/terms 上的使用条款。

你可以配置 npm 使用任何你喜欢的兼容的 registry，甚至运行你自己的 registry。其他人的
registry 的使用受他们的使用条款约束。

## 极简安装

npm 被打包在 [Node](https://nodejs.org/en/download/) 中。

### Windows 电脑

[获取 msi 安装包](https://nodejs.org/en/download/)。npm 包含在内。

### Apple 电脑

[获取 pkg 安装包](https://nodejs.org/en/download/)。npm 包含在内。

### 各种 Unix

运行 `make install`。npm 将会和 Node 一起安装。

如果你想要更高级的安装方式（不同版本，自定义路径等），请继续往下读。

## 高级安装 (Unix)

https://www.npmjs.com/install.sh 上有一个非常健壮的安装脚本。你可以下载后运行它。

这里是一个示例，使用了 curl：

```sh
curl -L https://www.npmjs.com/install.sh | sh
```

### 稍微高级

你可以为安装脚本设置配置参数：

```sh
npm_config_prefix=/some/path sh install.sh
```

或者你可以使用 debug 模式运行：

```sh
npm_debug=1 sh install.sh
```

### 更高级

使用 git 获取代码。使用 `make` 构建文档和其他东西。如果你打算修改 npm，`make link`
是你的朋友。

如果你已经获得 npm 源码，你也可以使用 `./configure --key=val ...` 设置任意非永久性的配置，
然后通过 `node bin/npm-cli.js <command> <args>` 运行 npm
命令。这在测试或者运行东西但不需要实际安装 npm 时很有帮助。

## 在 Windows 上安装或者升级

针对 Windows 用户的许多改进已经被包含在 npm 3 中——如果你运行最近版本的
npm，将获得更好的体验。如果想要升级，可以使用
[针对 Windows 的升级工具](https://github.com/felixrieseberg/npm-windows-upgrade) 
或者参考 [安装/升级 npm](https://npm.community/t/installing-upgrading-npm/251/2)
上的 Windows 升级说明。

如果这对你来说还不够高级，你也可以使用 git 获取代码，然后直接修改。

## 在 Cygwin 上安装

不支持。

## 卸载

看到你要走很伤心。

```sh
sudo npm uninstall npm -g
```

如果失败，还可以运行：

```sh
sudo make uninstall
```

## 更厉害的卸载

通常上面的说明已经足够了。它会移除 npm，但保留已经安装的东西。

如果你想要移除所有已经安装的包，你可以先使用 `npm ls` 命令找到它们，然后使用 `npm rm` 移除。

你可以使用 npm 中的 `clean-old.sh` 脚本来移除 npm 0.x
留下的碎片文件。可以很方便地运行，像这样：

```sh
npm explore npm -g -- sh scripts/clean-old.sh
```

npm 使用了两个配置文件，一个针对单用户，另一个针对全局（每个用户）。你可以像这样查看它们：

```sh
npm config get userconfig   # 默认指向 ~/.npmrc
npm config get globalconfig # 默认指向 /usr/local/etc/npmrc
```

卸载 npm 默认不会移除配置文件。如果你希望它们被删掉，必须自己手动移除。注意，这意味着将来 npm
安装时将无法记住你已经选择的设置。

## 更多文档

查看 [文档](https://docs.npmjs.com/)。

你可以使用 `npm help` 命令阅读任意一份文档。

如果你是一名开发者，想使用 npm 发布你的程序，你应该读
[这个](https://docs.npmjs.com/misc/developers)。

## 缺陷

当你发现问题时，请报告它们：

* web:
  <https://npm.community/c/bugs>

一定要包含不按预期工作的 npm 命令的 *所有* 输出内容。提供 `npm-debug.log` 文件也是很有用的。

你也可以在 https://package.community/ 或者
[Twitter](https://twitter.com/npm_support) 上通过 `#npm` 话题找到 npm
的人。回应的人很可能会告诉你通过 gist 或者电子邮件给出输出内容。

## 参见

* npm(1)
* npm-help(1)
* npm-index(7)
