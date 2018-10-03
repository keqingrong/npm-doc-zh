npm-ping(1) -- 检测 npm registry 连接
================================

## 概述

    npm ping [--registry <registry>]

## 描述

ping 配置的或者给定的 npm registry，检验身份验证。

如果成功了，会输出如下内容：

```
Ping success: {*Details about registry*}
```

否则输出：

```
Ping error: {*Detail about error}
```

## 参见

* npm-config(1)
* npm-config(7)
* npmrc(5)
