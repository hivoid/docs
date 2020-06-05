# Quick Start

[返回开发语言#Go](/language/?id=go)


## Go 语言环境

### 安装与配置

略

环境变量 GOROOT 会安装时默认配置为 go 的安装目录

配置 GOPATH 为需要的目录, 并添加配置 go 的 bin 目录, 添加以下代码到 `~/.bashrc`

```
export GOPATH="$HOME/go"
export GOBIN="$HOME/go/bin"
PATH="$PATH:$GOPATH/go/bin"
```

### 模块支持

>go 在版本 1.11 开始加入模块的支持, 1.14 成熟开始面向生产

模块的配置

环境变量 GO111MODULE 用来配置模块的支持与否, GO111MODULE 可以设置为以下四个值: `off`, `on`, `auto`, `""`

go 命令对于 go module 的支持情况如下:

1. "": 相当于默认值 auto, 详情查看 auto 项
2. on:  打开 module 模式, go命令将加载使用模块, 而不会在 GOPATH 下查找依赖, 而 GOPATH 仅仅用来存储源码包(在 $GOPATH/pkg/mod)和编译的可执行文件(在 $GOBIN 或 $GOPATH/bin)
3. off: 关闭 module 模式, 开启 GOPATH 模式, go命令将在 GOPATH 或 vendor 目录下查找依赖
4. auto: 默认值, 根据当前目录自动检测是否打开 module 模式, module 模式只有在当前目录包含 go.mod 文件或处于包含 go.mod 文件目录的下面的时候才会启用(1.13 开始，只要发现 go.mod 文件, 即使在 GOPATH 目录下也会激活 module 模式)

项目对 go module 的支持情况如下:

1. module-aware 模式: 项目可以建立在任意目录, go build 将会在 vendor 或根据 go.mod 配置来查找 import 引入的包, $GOPATH 不再被用来解析 import 指令
2. GOPATH 模式: 项目只能建立在 $GOPATH/src 目录下, import 引入的包也只能在 vendor 目录和 $GOPATH/src 目录下查找

_后边的项目默认启用模块支持_

## 创建项目

初始化一个模块项目

```
$ go mod init github.com/hiviod/algorithm
go: creating new go.mod: module github.com/hiviod/algorithm
```

写入代码

```
$ cat <<EOF > hello.go
package main

import (
    "fmt"
    "rsc.io/quote"
)

func main() {
    fmt.Println(quote.Hello())
}
EOF
```

编辑并执行

```
$ go build -o hello
go: finding module for package rsc.io/quote
go: downloading rsc.io/quote v1.5.2
go: found rsc.io/quote in rsc.io/quote v1.5.2
go: downloading rsc.io/sampler v1.3.0
go: downloading golang.org/x/text v0.0.0-20170915032832-14c0d48ead0c
$ ./hello
Hello, world.
```

go.mod 文件被更新, 加入了依赖包的配置, v1.5.2 是一个 semver tag:

```
$ cat go.mod
module github.com/hiviod/algorithm

go 1.14

require rsc.io/quote v1.5.2
```

更新依赖包到最新版本 go v1.13 开始 `go get -u` 不带参数仅更新当前包的依赖

```
$ go get -u ./...
go: rsc.io/sampler upgrade => v1.99.99
go: golang.org/x/text upgrade => v0.3.2
go: downloading rsc.io/sampler v1.99.99
go: downloading golang.org/x/text v0.3.2
```

go.mod 同时被更新

_文件中 `// indirect` 表示间接依赖，表示主项⽬直接依赖的包不是 module 模式时, 而此包又依赖的包(主项目不依赖), 或主项目依赖包的 go.mod 不完整时缺失的包_

```
$ cat go.mod
module github.com/hiviod/algorithm

go 1.14

require (
        golang.org/x/text v0.3.2 // indirect
        rsc.io/quote v1.5.2
        rsc.io/sampler v1.99.99 // indirect
)
```

引入更多依赖 `go get foo@v1.2.3, go get foo@master`

```
$ go get github.com/google/uuid
go: downloading github.com/google/uuid v1.1.1
go: github.com/google/uuid upgrade => v1.1.1
```
go.mod 文件同时更新增加了 `github.com/google/uuid v1.1.1 // indirect` 行到 require 区域

清除不再被依赖的模块

```
$ go mod tidy -v
unused github.com/google/uuid
```
go.mod 文件恢复到 `go get` 之前

创建包含依赖包的 vendor 目录

```
$ go mod vendor
$ ls -1F vendor
golang.org/
modules.txt
rsc.io/

```

如果依赖的包或模块出于一些原因暂不能发布到线上, 可以用 `replace` 指示引入本地目录
如果 replace 命令右边是一个文件系统的路径, 那目标目录下必须存在一个 go.mod 文件， 如果没有你可以用 `go mod init` 命令创建一个

`go mod why -m <mod>` 可看 `<mod>` 被依赖的关系路径, `<mod>` 为 `all` 时, 显示所有
