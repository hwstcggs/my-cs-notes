**Golang中引入error接口类型作为错误处理的标准模式，如果函数要返回错误，则返回值类型列表中肯定包含error。**

**触发和终止异常处理流程：**

* panic   // 触发

* recover // 终止

* defer来延迟执行defer后面的函数

  * 一个函数中执行多条defer语句
  * 执行顺序与声明顺序相反

**panic：**

* 停止当前函数执行
* 一直向上返回，执行每一层的defer
* 如果没有遇见recover，程序退出

**recover：**

* 仅在defer调用中使用
* 获取panic的值
* 如果无法处理，可重新panic

**error vs panic:**

* 意料之中的：使用error ，如：文件打不开等
* 意料之外的：使用panic，如：数组越界等

**实例：**

```
const prefix = "/list/"

type userError string

func (e userError) Error() string {
    return e.Message()
}

func (e userError) Message() string {
    return string(e)
}

func HandleFileList(writer http.ResponseWriter,request *http.Request) error {
    fmt.Println()
    if strings.Index( request.URL.Path, prefix) != 0 {
        return userError(fmt.Sprintf("path %s must start "+ "with %s",request.URL.Path, prefix))
    }
    path := request.URL.Path[len(prefix):] // 获取文件名
    file, err := os.Open(path)   // 打开文件
    if err != nil {
        return err
    }
    defer file.Close()

    all, err := ioutil.ReadAll(file) // 读取文件
    if err != nil {
        return err
    }

    writer.Write(all)
    return nil
}
```

```
type appHandler func(writer http.ResponseWriter,request *http.Request) error

func errWrapper(
    handler appHandler) func(http.ResponseWriter, *http.Request) {
        return func(writer http.ResponseWriter,
        request *http.Request) {
        // panic
        defer func() {
            if r := recover(); r != nil {
                log.Printf("Panic: %v", r)
                http.Error(writer,http.StatusText(http.StatusInternalServerError),http.StatusInternalServerError)
            }
        }() //匿名函数处理错误

        err := handler(writer, request)

        if err != nil {
            log.Printf("Error occurred "+"handling request: %s",err.Error()) // user error
            if userErr, ok := err.(userError); ok {http.Error(writer,userErr.Message(),http.StatusBadRequest)
                return
            } // system error
            code := http.StatusOK
            switch {
            case os.IsNotExist(err):
                code = http.StatusNotFound
            case os.IsPermission(err):
                code = http.StatusForbidden
            default:
                code = http.StatusInternalServerError
            }
            http.Error(writer,http.StatusText(code), code)
        }
    }
}

type userError interface {
    error
    Message() string
}

func main() {
    http.HandleFunc("/",errWrapper(HandleFileList))

    err := http.ListenAndServe(":8888", nil)
    if err != nil {
        panic(err)
    }
}
```



