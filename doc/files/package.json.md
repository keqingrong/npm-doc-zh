package.json(5) -- npm 的 package.json 处理细节
===========================================================

## 描述

本文档包含所有你需要知道的信息——package.json 文件需要什么。它必须是实际的 JSON，而不仅仅是
JavaScript 对象字面量。

`npm-config(7)` 中描述的配置设置会影响本文档中描述的许多行为。

## name（名称）

如果你计划发布你的包，package.json 中最重要的是要包含 name 和 version 字段（它们是必需的）。
name 和 version 一起构成唯一标识符。更新包的时候应该连同版本一起修改。如果你不打算发布你的包，
那么 name 和 version 字段都是可选的。

name 是包的名称。

一些规则：

* 名称必须少于或等于 214 个字符。包括限定范围的包（scoped package）中的范围（scope）。
* 名称不能以点或者下划线开头。
* 新包的名称不能有大写字母（译者注：早前允许名称中包含大写字母）。
* 名称最终会成为 URL 的一部分、命令行的参数，以及文件名。因此，名称不能包含任何非 URL 安全的字符。

（译者注：可以使用
[validate-npm-package-name](https://github.com/npm/validate-npm-package-name)
 检查包名是否合法。）

一些建议：

* 不要使用和 Node 核心模块相同的名称。
* 不要将 "js" 或 "node" 加入到到名称中。由于你在编写的是 package.json 文件，所以假定它是 JS，
  你可以使用 "engines" 字段指定引擎。（见下文）
* 因为名称可能会被作为参数传入 `require()` 函数，所以它应该简短，而且要描述合理。
* 在你使用喜欢的名称前，最好先检查 [npm registry](https://www.npmjs.com/)
  查看是否已经存在该名称。

名称前可以增加一个范围前缀，例如 `@myorg/mypackage`。更多细节见 `npm-scope(7)`。

## version（版本）

如果你计划发布你的包，package.json 中最重要的是要包含 name 和 version 字段（它们是必需的）。
name 和 version 一起构成唯一标识符。更新包的时候应该连同版本一起修改。如果你不打算发布你的包，
那么 name 和 version 字段都是可选的。

version 必须可以被 [node-semver](https://github.com/npm/node-semver) 解析，
它作为依赖被打包在 npm 中。（你可以通过 `npm install semver` 安装使用。）

更多版本号和版本范围的介绍见 semver(7)。

## description（描述）

填写包的文字描述信息。字符串类型。这有助于人们发现你的包，描述会在 `npm search` 中列出。

## keywords（关键词）

填写包的关键词信息。字符串数组类型。这有助于人们发现你的包，关键词会在 `npm search` 中列出。

## homepage（主页）

项目主页的 URL。

示例：

```json
{
  "homepage": "https://github.com/owner/project#readme"
}
```

## bugs（错误）

url 是项目的问题追踪系统网址，email 是报告问题的邮件地址。这些对使用你的包遇到问题的人很有帮助。

它应该像下面这样：

```json
{
  "bugs": {
    "url": "https://github.com/owner/project/issues",
    "email": "project@hostname.com"
  }
}
```

你可以指定一个或两个值。如果你想只提供一个 URL，可以将 "bugs" 的值指定为一个字符串，来代替对象。

如果提供了 "url"，`npm bugs` 命令会使用它。

## license（许可证）

你应该为你的包指定一个许可证，以便让人们知道他们的使用权利和你附加的限制。

如果你正在使用像 BSD-2-Clause 或 MIT 这样的通用许可证，为其添加一个当前的 SPDX 许可证标识符，
像这样：

```json
{
  "license": "BSD-3-Clause"
}
```

你可以检查 [完整的 SPDX 许可证标识符列表](https://spdx.org/licenses/)。

理想的情况下，你应该选一个 [OSI](https://opensource.org/licenses/alphabetical)
正式认可的许可证。

如果你的包是在多个通用许可证下被许可的，使用
[SPDX 许可证表达式语法 2.0 版](https://www.npmjs.com/package/spdx) 字符串，像这样：

```json
{
  "license": "(ISC OR GPL-3.0)"
}
```

如果你正在使用还没有被分配 SPDX 标识符的许可证，或者自定义的许可证，使用像这样的字符串值：

```json
{
  "license": "SEE LICENSE IN <filename>"
}
```

然后在包的顶级目录下包含一个命名为 `<filename>` 的文件。

一些旧的包使用 license 对象或者一个包含 license 对象数组的 "licenses" 属性：

```json
// 无效的元数据
{
  "license":
  {
    "type": "ISC",
    "url": "https://opensource.org/licenses/ISC"
  }
}
```

```json
// 无效的元数据
{
  "licenses": [
    {
      "type": "MIT",
      "url": "https://www.opensource.org/licenses/mit-license.php"
    },
    {
      "type": "Apache-2.0",
      "url": "https://opensource.org/licenses/apache2.0.php"
    }
  ]
}
```

这些风格现在已经被废弃了。取而代之的是使用 SPDX 表达式，像这样：

```json
{
  "license": "ISC"
}
```

```json
{
  "license": "(MIT OR Apache-2.0)"
}
```

最后，如果你不希望授予其他人在任何条件下使用私有包或者未发布的包的权利：

```json
{
  "license": "UNLICENSED"
}
```

也可以考虑设置 `"private": true` 避免意外发布。

## people fields: author, contributors（和人有关的字段：作者，贡献者）

"author" 是一个人，"contributors" 是一个 "person" 数组。"persion" 是一个对象，包含
"name" 字段和可选的 "url"、"email" 字段，像这样：

```json
{
  "name": "Barney Rubble",
  "email": "b@rubble.com",
  "url": "http://barnyrubble.tumblr.com/"
}
```

或者你可以把它们缩短成一个字符串，npm 会帮你解析：

```json
"Barney Rubble <b@rubble.com> (http://barnyrubble.tumblr.com/)"
```

无论哪种方式，email 和 url 都是可选的。

npm 也会使用你的 npm 用户信息来设置一个顶级的 "maintainers" 字段。

## files（文件）

`files` 字段是一个可选的文件模式数组，

The optional `files` field is an array of file patterns that describes
the entries to be included when your package is installed as a
dependency. File patterns follow a similar syntax to `.gitignore`, but
reversed: including a file, directory, or glob pattern (`*`, `**/*`, and such)
will make it so that file is included in the tarball when it's packed. Omitting
the field will make it default to `["*"]`, which means it will include all files.

Some special files and directories are also included or excluded regardless of
whether they exist in the `files` array (see below).

You can also provide a `.npmignore` file in the root of your package or
in subdirectories, which will keep files from being included. At the
root of your package it will not override the "files" field, but in
subdirectories it will. The `.npmignore` file works just like a
`.gitignore`. If there is a `.gitignore` file, and `.npmignore` is
missing, `.gitignore`'s contents will be used instead.

Files included with the "package.json#files" field _cannot_ be excluded
through `.npmignore` or `.gitignore`.

Certain files are always included, regardless of settings:

* `package.json`
* `README`
* `CHANGES` / `CHANGELOG` / `HISTORY`
* `LICENSE` / `LICENCE`
* `NOTICE`
* The file in the "main" field

`README`, `CHANGES`, `LICENSE` & `NOTICE` can have any case and extension.

Conversely, some files are always ignored:

* `.git`
* `CVS`
* `.svn`
* `.hg`
* `.lock-wscript`
* `.wafpickle-N`
* `.*.swp`
* `.DS_Store`
* `._*`
* `npm-debug.log`
* `.npmrc`
* `node_modules`
* `config.gypi`
* `*.orig`
* `package-lock.json` (use shrinkwrap instead)

## main

The main field is a module ID that is the primary entry point to your program.
That is, if your package is named `foo`, and a user installs it, and then does
`require("foo")`, then your main module's exports object will be returned.

This should be a module ID relative to the root of your package folder.

For most modules, it makes the most sense to have a main script and often not
much else.

## browser

If your module is meant to be used client-side the browser field should be
used instead of the main field. This is helpful to hint users that it might
rely on primitives that aren't available in Node.js modules. (e.g. `window`)

## bin

A lot of packages have one or more executable files that they'd like to
install into the PATH. npm makes this pretty easy (in fact, it uses this
feature to install the "npm" executable.)

To use this, supply a `bin` field in your package.json which is a map of
command name to local file name. On install, npm will symlink that file into
`prefix/bin` for global installs, or `./node_modules/.bin/` for local
installs.


For example, myapp could have this:

    { "bin" : { "myapp" : "./cli.js" } }

So, when you install myapp, it'll create a symlink from the `cli.js` script to
`/usr/local/bin/myapp`.

If you have a single executable, and its name should be the name
of the package, then you can just supply it as a string.  For example:

    { "name": "my-program"
    , "version": "1.2.5"
    , "bin": "./path/to/program" }

would be the same as this:

    { "name": "my-program"
    , "version": "1.2.5"
    , "bin" : { "my-program" : "./path/to/program" } }

Please make sure that your file(s) referenced in `bin` starts with
`#!/usr/bin/env node`, otherwise the scripts are started without the node
executable!

## man

Specify either a single file or an array of filenames to put in place for the
`man` program to find.

If only a single file is provided, then it's installed such that it is the
result from `man <pkgname>`, regardless of its actual filename.  For example:

    { "name" : "foo"
    , "version" : "1.2.3"
    , "description" : "A packaged foo fooer for fooing foos"
    , "main" : "foo.js"
    , "man" : "./man/doc.1"
    }

would link the `./man/doc.1` file in such that it is the target for `man foo`

If the filename doesn't start with the package name, then it's prefixed.
So, this:

    { "name" : "foo"
    , "version" : "1.2.3"
    , "description" : "A packaged foo fooer for fooing foos"
    , "main" : "foo.js"
    , "man" : [ "./man/foo.1", "./man/bar.1" ]
    }

will create files to do `man foo` and `man foo-bar`.

Man files must end with a number, and optionally a `.gz` suffix if they are
compressed.  The number dictates which man section the file is installed into.

    { "name" : "foo"
    , "version" : "1.2.3"
    , "description" : "A packaged foo fooer for fooing foos"
    , "main" : "foo.js"
    , "man" : [ "./man/foo.1", "./man/foo.2" ]
    }

will create entries for `man foo` and `man 2 foo`

## directories

The CommonJS [Packages](http://wiki.commonjs.org/wiki/Packages/1.0) spec details a
few ways that you can indicate the structure of your package using a `directories`
object. If you look at [npm's package.json](https://registry.npmjs.org/npm/latest),
you'll see that it has directories for doc, lib, and man.

In the future, this information may be used in other creative ways.

### directories.lib

Tell people where the bulk of your library is.  Nothing special is done
with the lib folder in any way, but it's useful meta info.

### directories.bin

If you specify a `bin` directory in `directories.bin`, all the files in
that folder will be added.

Because of the way the `bin` directive works, specifying both a
`bin` path and setting `directories.bin` is an error. If you want to
specify individual files, use `bin`, and for all the files in an
existing `bin` directory, use `directories.bin`.

### directories.man

A folder that is full of man pages.  Sugar to generate a "man" array by
walking the folder.

### directories.doc

Put markdown files in here.  Eventually, these will be displayed nicely,
maybe, someday.

### directories.example

Put example scripts in here.  Someday, it might be exposed in some clever way.

### directories.test

Put your tests in here. It is currently not exposed, but it might be in the
future.

## repository

Specify the place where your code lives. This is helpful for people who
want to contribute.  If the git repo is on GitHub, then the `npm docs`
command will be able to find you.

Do it like this:

    "repository": {
      "type" : "git",
      "url" : "https://github.com/npm/cli.git"
    }

    "repository": {
      "type" : "svn",
      "url" : "https://v8.googlecode.com/svn/trunk/"
    }

The URL should be a publicly available (perhaps read-only) url that can be handed
directly to a VCS program without any modification.  It should not be a url to an
html project page that you put in your browser.  It's for computers.

For GitHub, GitHub gist, Bitbucket, or GitLab repositories you can use the same
shortcut syntax you use for `npm install`:

    "repository": "npm/npm"

    "repository": "github:user/repo"

    "repository": "gist:11081aaa281"

    "repository": "bitbucket:user/repo"

    "repository": "gitlab:user/repo"

## scripts

The "scripts" property is a dictionary containing script commands that are run
at various times in the lifecycle of your package.  The key is the lifecycle
event, and the value is the command to run at that point.

See `npm-scripts(7)` to find out more about writing package scripts.

## config

A "config" object can be used to set configuration parameters used in package
scripts that persist across upgrades.  For instance, if a package had the
following:

    { "name" : "foo"
    , "config" : { "port" : "8080" } }

and then had a "start" command that then referenced the
`npm_package_config_port` environment variable, then the user could
override that by doing `npm config set foo:port 8001`.

See `npm-config(7)` and `npm-scripts(7)` for more on package
configs.

## dependencies

Dependencies are specified in a simple object that maps a package name to a
version range. The version range is a string which has one or more
space-separated descriptors.  Dependencies can also be identified with a
tarball or git URL.

**Please do not put test harnesses or transpilers in your
`dependencies` object.**  See `devDependencies`, below.

See semver(7) for more details about specifying version ranges.

* `version` Must match `version` exactly
* `>version` Must be greater than `version`
* `>=version` etc
* `<version`
* `<=version`
* `~version` "Approximately equivalent to version"  See semver(7)
* `^version` "Compatible with version"  See semver(7)
* `1.2.x` 1.2.0, 1.2.1, etc., but not 1.3.0
* `http://...` See 'URLs as Dependencies' below
* `*` Matches any version
* `""` (just an empty string) Same as `*`
* `version1 - version2` Same as `>=version1 <=version2`.
* `range1 || range2` Passes if either range1 or range2 are satisfied.
* `git...` See 'Git URLs as Dependencies' below
* `user/repo` See 'GitHub URLs' below
* `tag` A specific version tagged and published as `tag`  See `npm-dist-tag(1)`
* `path/path/path` See [Local Paths](#local-paths) below

For example, these are all valid:

    { "dependencies" :
      { "foo" : "1.0.0 - 2.9999.9999"
      , "bar" : ">=1.0.2 <2.1.2"
      , "baz" : ">1.0.2 <=2.3.4"
      , "boo" : "2.0.1"
      , "qux" : "<1.0.0 || >=2.3.1 <2.4.5 || >=2.5.2 <3.0.0"
      , "asd" : "http://asdf.com/asdf.tar.gz"
      , "til" : "~1.2"
      , "elf" : "~1.2.3"
      , "two" : "2.x"
      , "thr" : "3.3.x"
      , "lat" : "latest"
      , "dyl" : "file:../dyl"
      }
    }

### URLs as Dependencies

You may specify a tarball URL in place of a version range.

This tarball will be downloaded and installed locally to your package at
install time.

### Git URLs as Dependencies

Git urls are of the form:

    <protocol>://[<user>[:<password>]@]<hostname>[:<port>][:][/]<path>[#<commit-ish> | #semver:<semver>]

`<protocol>` is one of `git`, `git+ssh`, `git+http`, `git+https`, or
`git+file`.

If `#<commit-ish>` is provided, it will be used to clone exactly that
commit. If the commit-ish has the format `#semver:<semver>`, `<semver>` can
be any valid semver range or exact version, and npm will look for any tags
or refs matching that range in the remote repository, much as it would for a
registry dependency. If neither `#<commit-ish>` or `#semver:<semver>` is
specified, then `master` is used.

Examples:

    git+ssh://git@github.com:npm/cli.git#v1.0.27
    git+ssh://git@github.com:npm/cli#semver:^5.0
    git+https://isaacs@github.com/npm/cli.git
    git://github.com/npm/cli.git#v1.0.27

### GitHub URLs

As of version 1.1.65, you can refer to GitHub urls as just "foo":
"user/foo-project".  Just as with git URLs, a `commit-ish` suffix can be
included.  For example:

    {
      "name": "foo",
      "version": "0.0.0",
      "dependencies": {
        "express": "expressjs/express",
        "mocha": "mochajs/mocha#4727d357ea",
        "module": "user/repo#feature\/branch"
      }
    }

### Local Paths

As of version 2.0.0 you can provide a path to a local directory that contains a
package. Local paths can be saved using `npm install -S` or
`npm install --save`, using any of these forms:

    ../foo/bar
    ~/foo/bar
    ./foo/bar
    /foo/bar

in which case they will be normalized to a relative path and added to your
`package.json`. For example:

    {
      "name": "baz",
      "dependencies": {
        "bar": "file:../foo/bar"
      }
    }

This feature is helpful for local offline development and creating
tests that require npm installing where you don't want to hit an
external server, but should not be used when publishing packages
to the public registry.

## devDependencies

If someone is planning on downloading and using your module in their
program, then they probably don't want or need to download and build
the external test or documentation framework that you use.

In this case, it's best to map these additional items in a `devDependencies`
object.

These things will be installed when doing `npm link` or `npm install`
from the root of a package, and can be managed like any other npm
configuration param.  See `npm-config(7)` for more on the topic.

For build steps that are not platform-specific, such as compiling
CoffeeScript or other languages to JavaScript, use the `prepare`
script to do this, and make the required package a devDependency.

For example:

    { "name": "ethopia-waza",
      "description": "a delightfully fruity coffee varietal",
      "version": "1.2.3",
      "devDependencies": {
        "coffee-script": "~1.6.3"
      },
      "scripts": {
        "prepare": "coffee -o lib/ -c src/waza.coffee"
      },
      "main": "lib/waza.js"
    }

The `prepare` script will be run before publishing, so that users
can consume the functionality without requiring them to compile it
themselves.  In dev mode (ie, locally running `npm install`), it'll
run this script as well, so that you can test it easily.

## peerDependencies

In some cases, you want to express the compatibility of your package with a
host tool or library, while not necessarily doing a `require` of this host.
This is usually referred to as a *plugin*. Notably, your module may be exposing
a specific interface, expected and specified by the host documentation.

For example:

    {
      "name": "tea-latte",
      "version": "1.3.5",
      "peerDependencies": {
        "tea": "2.x"
      }
    }

This ensures your package `tea-latte` can be installed *along* with the second
major version of the host package `tea` only. `npm install tea-latte` could
possibly yield the following dependency graph:

    ├── tea-latte@1.3.5
    └── tea@2.2.0

**NOTE: npm versions 1 and 2 will automatically install `peerDependencies` if
they are not explicitly depended upon higher in the dependency tree. In the
next major version of npm (npm@3), this will no longer be the case. You will
receive a warning that the peerDependency is not installed instead.** The
behavior in npms 1 & 2 was frequently confusing and could easily put you into
dependency hell, a situation that npm is designed to avoid as much as possible.

Trying to install another plugin with a conflicting requirement will cause an
error. For this reason, make sure your plugin requirement is as broad as
possible, and not to lock it down to specific patch versions.

Assuming the host complies with [semver](https://semver.org/), only changes in
the host package's major version will break your plugin. Thus, if you've worked
with every 1.x version of the host package, use `"^1.0"` or `"1.x"` to express
this. If you depend on features introduced in 1.5.2, use `">= 1.5.2 < 2"`.

## bundledDependencies

This defines an array of package names that will be bundled when publishing
the package.

In cases where you need to preserve npm packages locally or have them
available through a single file download, you can bundle the packages in a
tarball file by specifying the package names in the `bundledDependencies`
array and executing `npm pack`.

For example:

If we define a package.json like this:

```
{
  "name": "awesome-web-framework",
  "version": "1.0.0",
  "bundledDependencies": [
    "renderized", "super-streams"
  ]
}
```
we can obtain `awesome-web-framework-1.0.0.tgz` file by running `npm pack`.
This file contains the dependencies `renderized` and `super-streams` which
can be installed in a new project by executing `npm install
awesome-web-framework-1.0.0.tgz`.

If this is spelled `"bundleDependencies"`, then that is also honored.

## optionalDependencies

If a dependency can be used, but you would like npm to proceed if it cannot be
found or fails to install, then you may put it in the `optionalDependencies`
object.  This is a map of package name to version or url, just like the
`dependencies` object.  The difference is that build failures do not cause
installation to fail.

It is still your program's responsibility to handle the lack of the
dependency.  For example, something like this:

    try {
      var foo = require('foo')
      var fooVersion = require('foo/package.json').version
    } catch (er) {
      foo = null
    }
    if ( notGoodFooVersion(fooVersion) ) {
      foo = null
    }

    // .. then later in your program ..

    if (foo) {
      foo.doFooThings()
    }

Entries in `optionalDependencies` will override entries of the same name in
`dependencies`, so it's usually best to only put in one place.

## engines

You can specify the version of node that your stuff works on:

    { "engines" : { "node" : ">=0.10.3 <0.12" } }

And, like with dependencies, if you don't specify the version (or if you
specify "\*" as the version), then any version of node will do.

If you specify an "engines" field, then npm will require that "node" be
somewhere on that list. If "engines" is omitted, then npm will just assume
that it works on node.

You can also use the "engines" field to specify which versions of npm
are capable of properly installing your program.  For example:

    { "engines" : { "npm" : "~1.0.20" } }

Unless the user has set the `engine-strict` config flag, this
field is advisory only and will only produce warnings when your package is installed as a dependency.

## engineStrict

**This feature was removed in npm 3.0.0**

Prior to npm 3.0.0, this feature was used to treat this package as if the
user had set `engine-strict`. It is no longer used.

## os

You can specify which operating systems your
module will run on:

    "os" : [ "darwin", "linux" ]

You can also blacklist instead of whitelist operating systems,
just prepend the blacklisted os with a '!':

    "os" : [ "!win32" ]

The host operating system is determined by `process.platform`

It is allowed to both blacklist, and whitelist, although there isn't any
good reason to do this.

## cpu

If your code only runs on certain cpu architectures,
you can specify which ones.

    "cpu" : [ "x64", "ia32" ]

Like the `os` option, you can also blacklist architectures:

    "cpu" : [ "!arm", "!mips" ]

The host architecture is determined by `process.arch`

## preferGlobal

**DEPRECATED**

This option used to trigger an npm warning, but it will no longer warn. It is
purely there for informational purposes. It is now recommended that you install
any binaries as local devDependencies wherever possible.

## private

If you set `"private": true` in your package.json, then npm will refuse
to publish it.

This is a way to prevent accidental publication of private repositories.  If
you would like to ensure that a given package is only ever published to a
specific registry (for example, an internal registry), then use the
`publishConfig` dictionary described below to override the `registry` config
param at publish-time.

## publishConfig

This is a set of config values that will be used at publish-time. It's
especially handy if you want to set the tag, registry or access, so that
you can ensure that a given package is not tagged with "latest", published
to the global public registry or that a scoped module is private by default.

Any config values can be overridden, but only "tag", "registry" and "access"
probably matter for the purposes of publishing.

See `npm-config(7)` to see the list of config options that can be
overridden.

## DEFAULT VALUES

npm will default some values based on package contents.

* `"scripts": {"start": "node server.js"}`

  If there is a `server.js` file in the root of your package, then npm
  will default the `start` command to `node server.js`.

* `"scripts":{"install": "node-gyp rebuild"}`

  If there is a `binding.gyp` file in the root of your package and you have not defined an `install` or `preinstall` script, npm will
  default the `install` command to compile using node-gyp.

* `"contributors": [...]`

  If there is an `AUTHORS` file in the root of your package, npm will
  treat each line as a `Name <email> (url)` format, where email and url
  are optional.  Lines which start with a `#` or are blank, will be
  ignored.

## SEE ALSO

* semver(7)
* npm-init(1)
* npm-version(1)
* npm-config(1)
* npm-config(7)
* npm-help(1)
* npm-install(1)
* npm-publish(1)
* npm-uninstall(1)
