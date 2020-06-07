# 问题记录

## 开发环境搭建

**VS Code 和 gopls**

* 问题1: 多 module 无法自动适配, 参考 (issue)[https://github.com/golang/go/issues/32394] , 可暂时为每个 module 配置一个 workspace。
* 问题2: package 行提示: "...is not part of a package LSP", 可能和问题1同样的原因造成，也可能是手动配置的 GOPATH, 而 VSCode 依然把 $HOME/go 当作默认 GOPATH 造成的。
