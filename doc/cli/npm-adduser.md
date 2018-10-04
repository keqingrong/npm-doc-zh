npm-adduser(1) -- 增加一个 registry 用户账号
=============================================

## 概述

    npm adduser [--registry=url] [--scope=@orgname] [--always-auth] [--auth-type=legacy]

    别名: login, add-user

## 描述

在指定 registry 中创建或者验证名为 `<username>` 的用户，将证书保存到 `.npmrc` 文件中。
如果没有指定 registry，将会使用默认的 registry，见 `npm-config(7)`。

用户名、密码和电子邮件都会从提示符（prompt）读取。

要重置密码，访问 <https://www.npmjs.com/forgot>。

要修改电子邮件地址，访问 <https://www.npmjs.com/email-edit>。

你可能会多次使用这个命令和相同的用户账号授权新的机器。
授权一台新机器时，用户名、密码和电子邮件地址都必须匹配现有记录。

`npm login` 是 `npm adduser` 的别名，行为完全一致。

## 配置

### registry

默认值: `https://registry.npmjs.org/`

npm 包 registry 的基础 URL。如果指定了 `scope`，该 registry 将只会用于使用该 `scope`
的包。如果有的话，`scope` 默认是你当前所在项目目录的 `scope`。参见 `npm-scope(7)`。

### scope

默认值: 无

如果指定，那么用户和登录证书将会关联到该 `scope`。参见 `npm-scope(7)`。你可以同时使用，例如：

```sh
npm adduser --registry=http://myregistry.example.com --scope=@myco
```

这会为给定的 `scope` 设置一个 registry，并且同时针对该 registry 登录或者创建一个用户。

### always-auth

默认值: `false`

如果指定，会保存该配置，指明所有到给定 registry 的请求都应该包含认证信息。对私有 registry
很有用。可以和 `--registry` 及 / 或 `--scope` 一起使用，例如：

```sh
npm adduser --registry=http://private-registry.example.com --always-auth
```

这将确保所有到 registry 的请求（包括 tarball）都包含认证头。该设置对使用私有 registry
（元数据和包的压缩包存储在有不同的主机名的主机上）来说可能是必要的。`always-auth`
的更多细节，参见 `npm-config(7)` 中的 `always-auth`。`always-auth`
的指定 registry 配置（registry-specific configuration）优先于任何全局配置。

### auth-type

* 默认值: `'legacy'`
* 类型: `'legacy'`, `'sso'`, `'saml'`, `'oauth'`

和 `adduser`/`login` 一起使用的身份认证策略。一些 npm registry（例如 npmE），除了传统 npm
中经典的用户名/密码，可能还支持另外的身份认证策略。

译者注：npmE 即 [npm Enterprise](https://www.npm-enterprise.com/)。

## 参见

* npm-registry(7)
* npm-config(1)
* npm-config(7)
* npmrc(5)
* npm-owner(1)
* npm-whoami(1)
