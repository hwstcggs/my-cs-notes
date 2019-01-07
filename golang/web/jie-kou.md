* ##### duck typing

python 中：

```
def download(retriever):
    return retriever.get("www.google.com")
```

1. 运行时才知道传入的retriever有没有get方法
2. 需要注释来说明接口

* ##### 接口的定义和实现

interface是一组method签名的组合，我们通过interface来定义对象的一组行为;

interface类型定义了一组方法，如果某个对象实现了某个接口的所有方法，则此对象就实现了此接口;

```
type Retriever struct {
    Contents string
}

func (r *Retriever) String() string {
    return fmt.Sprintf(
        "Retriever: {Contents=%s}", r.Contents)
}

func (r *Retriever) Post(url string,
    form map[string]string) string {
    r.Contents = form["contents"]
    return "ok"
}

func (r *Retriever) Get(url string) string {
    return r.Contents
}

type Retriever interface {
    Get(url string) string
}

type Poster interface {
    Post(url string,
        form map[string]string) string
}

const url = "http://www.imooc.com"

func download(r Retriever) string {
    return r.Get(url)
}

func post(poster Poster) {
    poster.Post(url,
        map[string]string{
            "name":   "ccmouse",
            "course": "golang",
        })
}

type RetrieverPoster interface {
    Retriever
    Poster
}

func session(s RetrieverPoster) string {
    s.Post(url, map[string]string{
        "contents": "another faked imooc.com",
    })
    return s.Get(url)
}

func main() {
    var r Retriever

    mockRetriever := mock.Retriever{
        Contents: "this is a fake imooc.com"}
    r = &mockRetriever
    inspect(r)

    r = &real.Retriever{
        UserAgent: "Mozilla/5.0",
        TimeOut:   time.Minute,
    }
    inspect(r)

    // Type assertion
    if mockRetriever, ok := r.(*mock.Retriever); ok {
        fmt.Println(mockRetriever.Contents)
    } else {
        fmt.Println("r is not a mock retriever")
    }

    fmt.Println(
        "Try a session with mockRetriever")
    fmt.Println(session(&mockRetriever))
}

func inspect(r Retriever) {
    fmt.Println("Inspecting", r)
    fmt.Printf(" > Type:%T Value:%v\n", r, r)
    fmt.Print(" > Type switch: ")
    switch v := r.(type) {
    case *mock.Retriever:
        fmt.Println("Contents:", v.Contents)
    case *real.Retriever:
        fmt.Println("UserAgent:", v.UserAgent)
    }
    fmt.Println()
}
```

* ##### 接口的值类型

* ##### 接口的组合

* ##### 常用系统接口



