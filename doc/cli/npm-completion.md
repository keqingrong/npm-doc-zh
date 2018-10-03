npm-completion(1) -- npm Tab 补全
===========================================

## 概述

    source <(npm completion)

## 描述

在所有的 npm 命令中启用 tab 补全。

上面概述中的命令会将自动补全加载到你当前的 shell 中。将它加到你的 `~/.bashrc` 或者
`~/.zshrc` 中，将会使自动补全随处可用。

```sh
npm completion >> ~/.bashrc
npm completion >> ~/.zshrc
```

你当然也可以将 `npm completion` 的输出通过管道导到文件中，例如
`/usr/local/etc/bash_completion.d/npm`（如果你有一个系统将会帮你读取该文件）。

当环境中定义了 `COMP_CWORD`、`COMP_LINE`、`COMP_POINT` 时，`npm completion`
会进入 "plumbing mode" 模式，基于参数输出补全。

## 参见

* npm-developers(7)
* npm(1)
