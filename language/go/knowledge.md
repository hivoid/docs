# 知识点

[返回开发语言#Go](/language/?id=go)


## Context

结构定义

```go
type Context interface {
    // 返回此上下文相关任务完成(应该调用cancel时)的时间, 如果没有设置 deadline, ok=false
	Deadline() (deadline time.Time, ok bool)

    // 返回一个用于关闭程序的 channel, 上下文相关任务完成时, 此 channel 会被关闭
    // 如果上下文不能被取消则返回 nil
    // channel 的关闭可能会在 cancel() 返回后异步完成
    //
    // `WithCancel` 返回的上下文，额外会在 cancel() 调用后执行关闭 channel
    // `WithDeadlin`和`WithTimeout` 额外会在超时后执行关闭 chancel
	//
	// Done 通常会结合 select 语句一起使用:
	Done() <-chan struct{}

	// 如果 Done 没有关闭返回 nil.
	// 如果 Done 已经关闭返回 携带上下文被取消或Deadline超时信息的error.
	Err() error

	// 用来返回(一般是 WithValue 存储的) key 对应的 value, 如果 key 不存在返回 nil
	// 应该仅用于进程间和API边界请求范围内的数据, 不可滥用, 比如给函数传递可选参数
	Value(key interface{}) interface{}
}
```

获取顶级上下文

```go
// 获取顶级上下文
ctx := context.Background()
```

获取新上下文

```go
// 获取带有新 Done Channel 的父上下文副本上下文
// cancel 的调用会关闭这个 Done Channel，父上下文 Done Channel 的关闭也会导致此上下文的 Done Channel 关闭
// cancel 会释放此上下文关联的所有资源，故此上下文相关操作完成的时候应该尽快调用 cancel
ctx, cancel := context.WithCancel(context.Background())
```

获取自动超时的新上下文

```go
// 获取上下文同 WithCancel, 但是超时会自动调用 cancel
ctx, cancel := context.WithTimeout(context.Background())
```

优雅的关闭程序

```go
// 创建用于接收系统信号的 channel
quit := make(chan os.Signal)
// 设置将 os.Interrupt 信号传递到 quit channel
signal.Notify(quit, os.Interrupt)
// 等待系统信号
<-quit
// 收到中断信号，执行退出程序
ctx, cancel := context.WithTimeout(context.Background(), 20*time.Second)
defer cancel()

// 优雅的关闭程序
// 先关闭 listeners，后关闭空闲连接，最后等待活动连接空闲后将其关闭，如果一直有则一直等待
// 如果等待过程中 ctx 在关闭完成前过期则返回 ctx 的 error, 否则返回关闭 listeners 过程中的错误
if err := s.Shutdown(ctx); err != nil {
    log.Fatal(err)
}
```

## 概念

**闭包 (Closure)**
>闭包是对词法闭包(Lexical Closure)的简称, 当一个函数在其词法上下文中引用了自由变量, 则此函数和其引用环境组成的整体就叫做闭包 

**高阶函数 (Higher-order function)**
>高阶函数是指使用其他函数作为参数、或者返回一个函数作为结果的函数, 至少满足下列一个条件:
> * 接受一个或多个函数作为输入
> * 输出一个函数