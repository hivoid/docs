# 开发与生产

[返回开发语言#Go](/language/?id=go)

## 平滑重启

**原理**

1. 监听信号（USR2..）
2. 收到信号时fork子进程（使用相同的启动命令），将服务监听的socket文件描述符传递给子进程
3. 子进程监听父进程的socket，这个时候父进程和子进程都可以接收请求
4. 子进程启动成功之后，父进程停止接收新的连接，等待旧连接处理完成（或超时）
5. 父进程退出，重启完成

**细节**

1. 父进程将socket文件描述符传递给子进程可以通过命令行，或者环境变量等
2. 子进程启动时使用和父进程一样的命令行，对于golang来说用更新的可执行程序覆盖旧程序
3. server.Shutdown()优雅关闭方法是go>=1.8的新特性
4. server.Serve(l)方法在Shutdown时立即返回，Shutdown方法则阻塞至context完成，所以Shutdown的方法要写在主goroutine中

**可用服务**

* [grace](https://github.com/facebookarchive/grace)
* [endless](https://github.com/fvbock/endless)
* [overseer](https://github.com/jpillora/overseer)

## 服务进程管理

**Work with systemd**

**Work with supervisor**

## 维护

* [pprof](https://github.com/google/pprof) | [a blog](https://eddycjy.com/posts/go/tools/2018-09-15-go-tool-pprof/) 性能监控分析
* runtime/trace 运行时信息追踪
