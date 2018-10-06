npm-audit(1) -- 运行安全审计
====================================

## 概述

    npm audit [--json|--parseable]
    npm audit fix [--force|--package-lock-only|--dry-run|--production|--only=dev]

## 示例

扫描项目漏洞，为易受攻击的依赖自动安装兼容更新。

```sh
$ npm audit fix
```

运行 `audit fix` ，但不修改 `node_modules`，只更新锁文件：

```sh
$ npm audit fix --package-lock-only
```

跳过更新 `devDependencies`：

```sh
$ npm audit fix --only=prod
```

使用 `audit fix` 将语义化版本主版本更新安装为顶级依赖，不仅仅是兼容的语义化版本：

```sh
$ npm audit fix --force
```

进行空运行（dry run），从而了解 `audit fix` 会做什么，*也* 支持以 JSON 格式输出安装信息：

```sh
$ npm audit fix --dry-run --json
```

扫描项目漏洞，仅显示细节，不会进行修复：

```sh
$ npm audit
```

使用 JSON 格式显示详细的审计报告：

```sh
$ npm audit --json
```

使用纯文本格式展示详细的审计报告，用制表符分隔，允许未来在脚本或者命令行后处理中复用，
例如选择打印某些列：

```sh
$ npm audit --parseable
```

如果要解析列，你可以使用像 `awk` 这样的工具，仅打印其中的一部分：

```sh
$ npm audit --parseable | awk -F $'\t' '{print $1,$4}'
```

## 描述

`audit` 命令会提交依赖（项目配置的）描述到默认的 registry，请求一份已知漏洞的报告。
该报告返回内容包含根据该信息如何采取行动的说明。

你也可以通过运行 `npm audit fix` 让 npm 自动修复漏洞。注意，一些漏洞不能被自动修复，需要手动
干预或者评审。同样需要注意的是，由于 `npm audit fix` 会在底层运行 `npm install`，所有应用到
安装器的配置也会应用到 `npm install`——所以 `npm audit fix --package-lock-only` 会按预
期工作。

## 内容提交

* npm 版本（npm_version）
* Node 版本（node_version）
* 平台（platform）
* Node 环境变量（node_env）
* 从你的 package-lock.json 或 npm-shrinkwrap.json 中清洗出来的版本

### 清洗

为了确保潜在的敏感信息不会被包含在审计数据包中，一些依赖的名称（有时候是版本）可能会被替换为不透明
不可逆的标识符。这样做是为了以下依赖类型：

* 任何引用限定范围（scope）的模块（被配置为非默认 registry），名称会被清洗。换言之，限定范围
（scope）对 `npm login --scope=@ourscope` 有效。
* 所有的 git 依赖，名称和说明符会被清洗。
* 所有的远程压缩包依赖，名称和说明符会被清洗。
* 所有的本地目录和压缩包依赖，名称和说明符会被清洗。

不可逆的标识符是会话特定的 UUID 和被替换值的 sha256 值，确保不同运行时的载荷（payload）是一致
的值。

## 参见

* npm-install(1)
* package-locks(5)
* config(7)
