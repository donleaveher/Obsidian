## Download
```bash
go get -u github.com/gin-gonic/gin
```

## The basic Application
```go
package main

import (
    "net/http"
    "github.com/gin-gonic/gin"
)
func main() {
    // 1. 创建一个默认的路由引擎
    // Default() 包含了 Logger 和 Recovery 中间件
    r := gin.Default()

    // 2. 定义一个 GET 请求的路由
    // c *gin.Context 是 Gin 的核心，封装了 Request 和 Response
    r.GET("/hello", func(c *gin.Context) {
        // 返回 JSON 格式的数据到客户端
        c.JSON(http.StatusOK, gin.H{
            "message": "Hello, Gin!",
            "status":  "success",
        })
	    // resp 是一个返回到内容
	     c.JSON(http.StatusOK, resp)
    })
    // 3. 启动 HTTP 服务，默认在 0.0.0.0:8080 启动
    r.Run(":8080") 
}
```
***Logger***
- 记录每一次 API 请求的详细信息, 并输出到控制台（终端）
```bash
[GIN] 2023/12/08 - 10:00:00 | 200 |  152.4µs |  127.0.0.1 | GET  "/hello"  
```
- **时间** (`2023/12/08...`)：请求是什么时候发生的。
- **状态码** (`200`)：请求成功了还是失败了（200 OK, 404 Not Found, 500, Error 等）。
	- Gin 会自动把成功的标绿，失败的标红，方便查看。
- **耗时** (`152.4µs`)：处理这个请求花了多久（这对性能优化至关重要）。
- **客户端 IP** (`127.0.0.1`)：是谁发起的请求。
- **方法与路径** (`GET "/hello"`)：请求了哪个接口。
***Recovery***
- 防止程序崩溃
```go
r.GET("/bomb", func(c *gin.Context) {
    // 模拟一个严重错误
    panic("糟糕！服务器内部爆炸了！") 
})
```
**Recovery 的工作流程：**
1. 它就像一张“安全网”，包裹在你的每一个请求处理函数外面。
2. 如果你的业务代码（比如连接数据库失败、逻辑错误）触发了 `panic`。
3. **Recovery** 会捕获这个 panic，阻止程序崩溃。
4. 它会打印错误的**堆栈信息**（Stack Trace）到日志，方便你修 bug。
5. 它会自动给前端返回一个 **500 Internal Server Error**，而不是让连接断开。

## Get Parameter
### Get URL Path Parameters
```go
r.GET("/user/:name", func(c *gin.Context) {
	// The "name" is correspond with "/:name"
    name := c.Param("name")
    c.String(http.StatusOK, "Hello %s", name)
})
```

### Get URL Query String
```go
Input Format: /search?q=golang&page=1
r.GET("/search", func(c *gin.Context) {
    // 获取 q 参数，如果没有则默认为 "nothing"
    q := c.DefaultQuery("q", "nothing") 
    page := c.Query("page")

    c.JSON(http.StatusOK, gin.H{
        "query": q,
        "page":  page,
    })
})
```

### Get Post/Json Data (Binding)
```go
type LoginRequest struct {
	User string `json:"user" binding:"required"` // binding:"required" 表示必填
	Password string `json:"password" binding:"required"`
}

r.POST("/login", func(c *gin.Context) {
	var json LoginRequest
	// ShouldBindJSON 尝试将请求体解析为 JSON 并绑定到结构体
	if err := c.ShouldBindJSON(&json); err != nil {
		c.JSON(http.StatusBadRequest, gin.H{"error": err.Error()})
		return
	}
	// 逻辑处理...
	if json.User == "admin" && json.Password == "123456" {
		c.JSON(http.StatusOK, gin.H{"status": "you are logged in"})
	} else {
		c.JSON(http.StatusUnauthorized, gin.H{"status": "unauthorized"})
	}
})
```

***Using Postman to Send Post requirement***
- **新建请求**：点击 "+" 号。
- **方法**：下拉选择 **POST**。
- **URL**：填入 `http://localhost:8080/login`。
- **Body (请求体)**：
    - 选择 **Raw**。
    - 右边格式选择 **JSON**。
    - 在框里粘贴上面的 JSON 代码。
- **发送**：点击 Send，下面会显示响应结果。
***Using Terminal to Send Post requirement***
```bash
curl -X POST http://localhost:8080/login \
  -H "Content-Type: application/json" \
  -d '{"user": "admin", "password": "123456"}'
```

***Tip***
The Defination of struct
```go
User string `json:"user" ...`
```
- **Go 里面**：字段名 `User` 首字母必须**大写**（为了让外部包能访问）。
- **JSON 里面**：因为你加了标签 `` `json:"user"` ``，所以前端传过来的 JSON key 必须是**小写**的 `"user"`。
- **测试**：如果你发 `{"User": "admin"}` (大写U)，Gin 会因为找不到匹配的标签而忽略它，导致报错 "Field validation for 'User' failed on the 'required' tag"。

Content-Type
发送请求时，HTTP Header 里的 `Content-Type` 必须是 **`application/json`**。
- `ShouldBindJSON` 会检查这个头部。如果没设置，它可能无法正确解析。Postman 选 "JSON" 模式会自动帮你加上这个头。
在现代 Web 开发（RESTful API）中，**严格规定 Content-Type 是标准规范**。
- **application/json**：告诉服务器我是 JSON。
- **text/html**：告诉浏览器我是网页。
- **image/png**：告诉浏览器我是图片。

## The Life Circle of Gin (Middleware)
Gin 的中间件（Middleware）机制非常灵活。你可以把中间件看作是请求处理链条上的“拦截器”。它们可以在请求到达最终处理函数**之前**或**之后**执行逻辑（如日志记录、鉴权、跨域处理）。
```go
func MyLogger() gin.HandlerFunc {
    return func(c *gin.Context) {
        // --- 第一阶段：进门（请求前逻辑） ---
        // 这里就像安检口。请求刚进来，还没到具体的 API。
        // 我们利用 Context (c) 这个“大背包”，往里面塞了一个数据。
        c.Set("example", "12345")

        // --- 第二阶段：放行（核心控制点） ---
        // c.Next() 是最关键的一行！
        // 它的意思是：“我（中间件）的事先做完了，该轮到下一个中间件或者最终的路由函数了，请继续执行
        // 此时，程序会跳出当前的函数，去执行 r.GET("/test", ...) 里的代码。
        c.Next() 
        
        // --- 第三阶段：回头（请求后逻辑） ---
        // 这里的代码，会在 r.GET("/test", ...) 执行**完毕**之后，才会执行！
        // 就像回力标一样，程序处理完业务逻辑，又回到了这里。
        status := c.Writer.Status()
        println("请求结束，状态码:", status)
    }
}

func main() {
	r := gin.New()
	r.Use(MyLogger()) // 全局注册中间件
	
	r.GET("/test", func(c *gin.Context) {
	// 这里的 c 和中间件里的 c 是同一个对象（同一个背包） 
	// 1. 打开背包，拿出中间件里放进去的 "example" 
	// 2. .(string) 是 Go 的类型断言，因为取出来的是 interface{}（任意类型），必须告诉 Go 它是         string
		example := c.MustGet("example").(string)
		c.JSON(200, gin.H{"example": example})
	})
	r.Run()
}
```
***Pipeline***
当你访问 `http://localhost:8080/test` 时，程序内部是这样跑的：
1. **用户发起请求**。
    
2. 进入 `MyLogger` 中间件。
    
3. 执行 `c.Set("example", "12345")` —— **数据装包**。
    
4. 遇到 `c.Next()` —— **暂停，移交控制权**。
    
5. 进入 `r.GET("/test")` 的匿名函数。
    
6. 执行 `c.MustGet("example")` —— **拿到数据**。
    
7. 执行 `c.JSON(...)` —— **发送响应给浏览器**。
    
8. `r.GET` 函数结束，控制权**弹回**给 `MyLogger`。
    
9. 继续执行 `c.Next()` 下面的代码。
    
10. 执行 `println(...)` —— **打印日志**。
    
11. **请求彻底结束**。

## Grouping
当 API 变多时，你需要对路由进行分组管理（例如区分版本 v1, v2）。
```go
func main() {
    r := gin.Default()

    // 创建 v1 路由组
    v1 := r.Group("/v1")
    {
        v1.GET("/login", loginEndpoint)
        v1.GET("/submit", submitEndpoint)
        v1.POST("/read", readEndpoint)
    }

    // 创建 v2 路由组
    v2 := r.Group("/v2")
    {
        v2.POST("/login", loginEndpointV2)
    }
    r.Run()
}
```
***Tips:*** LoginEndpoint | SubmitEndpoint | ReadEndpoint | LoginEndpointV2 are `gin.HandlerFunc`type function
```go
// 对应 v1.GET("/login", loginEndpoint)
func loginEndpoint(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{
        "version": "v1",
        "action":  "login",
        "message": "正在使用 V1 版本登录...",
    })
}

// 对应 v1.GET("/submit", submitEndpoint)
func submitEndpoint(c *gin.Context) {
    c.String(http.StatusOK, "V1 提交成功")
}

// 对应 v1.POST("/read", readEndpoint)
func readEndpoint(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{"data": "V1 读取数据"})
}

// 对应 v2.POST("/login", loginEndpointV2)
func loginEndpointV2(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{
        "version": "v2", 
        "action":  "login",
        "message": "欢迎！这是更高级的 V2 版本登录", // 逻辑变了
    })
}
```