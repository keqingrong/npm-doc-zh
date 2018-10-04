npm-access(1) -- 设置已发布的包的访问级别
=======================================================

## 概述

    npm access public [<package>]
    npm access restricted [<package>]

    npm access grant <read-only|read-write> <scope:team> [<package>]
    npm access revoke <scope:team> [<package>]

    npm access ls-packages [<user>|<scope>|<scope:team>]
    npm access ls-collaborators [<package> [<user>]]
    npm access edit [<package>]

## 描述

用于设置私有包的访问控制。

对于所有的子命令，如果没有传入包名， `npm access` 将会在当前工作目录执行动作。

* public/restricted:
  将包设置为公开访问或者受限制的。
* grant/revoke:
  增加或者移除用户和团队对包的只读或者可读写访问能力。
* ls-packages:
  显示用户或者团队能访问的所有包，及访问级别，除了只读的公开包（它不会打印整个 registry 列表）。
* ls-collaborators:
  显示包的所有访问权限。只显示你至少有读权限的包的权限。如果传了
  `<user>`，列表将会被过滤，只针对用户所属的*那个*团队。
* edit:
  使用 `$EDITOR` 立即设置包的访问权限。

## 细节

`npm access` 总是直接操作当前的 registry，可以在命令行通过 `--registry=<registry url>`
配置。

没有限定范围的包（unscoped package）*始终是公开的*。

限定范围的包（scoped package）*默认是受限制的*，但你可以通过
`npm publish --access=public` 发布为公开的，或者在初次发布后通过 `npm access public`
设置为公开访问。

你必须有权限设置包的访问级别：

* 你是一个没有限定范围或者限定范围的包的所有者。
* 你是拥有限定范围的团队的成员。
* 你已经被赋予一个包的可读写权限，无论是作为团队的成员还是直接是所有者。

如果你启用了两步认证（two-factor authentication），当访问级别变更时必须使用 `--otp`
传入一次性密码（OPT, One-time Password）。

如果你的账户是未付费的，尝试发布限定范围的包将会失败，返回 HTTP 402
状态码（逻辑上讲），除非你使用 `--access=public`。

使用 `npm team` 命令完成团队和团队成员的管理。

## 参见

* npm-team(1)
* npm-publish(1)
* npm-config(7)
* npm-registry(7)
