# gin framework

## 注意事项

**在中间件里使用 goroutine**

```go
r.GET("/long_async", func(c *gin.Context) {
		// 创建在 goroutine 中使用的副本
		cCp := c.Copy()
		go func() {
			// 用 time.Sleep() 模拟一个长任务。
			time.Sleep(5 * time.Second)

			// 请注意您使用的是复制的上下文 "cCp"，这一点很重要
			log.Println("Done! in path " + cCp.Request.URL.Path)
		}()
	})
```

**将 request body 绑定到不同的结构体中**

* c.ShouldBind 使用了 c.Request.Body, 并将其设置为 EOF，不可重用。
* c.ShouldBindBodyWith 会在绑定之前将 body 存储到上下文中。 这会对性能造成轻微影响，如果调用一次就能完成绑定的话，那就不要用这个方法。
* 只有某些格式需要此功能，如 JSON, XML, MsgPack, ProtoBuf。 对于其他格式, 如 Query, Form, FormPost, FormMultipart 可以多次调用 c.ShouldBind() 而不会造成任任何性能损失 

```go
func SomeHandler(c *gin.Context) {
    objA := formA{}
    objB := formB{}
    // 读取 c.Request.Body 并将结果存入上下文。
    if errA := c.ShouldBindBodyWith(&objA, binding.JSON); errA == nil {
        c.String(http.StatusOK, `the body should be formA`)
        // 这时, 复用存储在上下文中的 body。
    } else if errB := c.ShouldBindBodyWith(&objB, binding.JSON); errB == nil {
        c.String(http.StatusOK, `the body should be formB JSON`)
        // 可以接受其他格式
    } else if errB2 := c.ShouldBindBodyWith(&objB, binding.XML); errB2 == nil {
        c.String(http.StatusOK, `the body should be formB XML`)
    } else {
    ...
    }
}
```