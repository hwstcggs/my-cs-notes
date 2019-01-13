协程 Coroutine

* 轻量级“线程”
* 非抢占式多任务处理，由协程主动交出控制权
* 编译器/解释器/虚拟机层面的多任务
* 多个协程可能在一个或多个线程上运行

```
func main(){
   var a [10] int
   for i := 0;i<10;i++{
      go func(j int){
          for {
             a[j]++
             runtime.Gosched() // 主动交出控制权
          } 
      }(i)
   }
   time.sleep(time.Millsecond)
   fmt.Println(a)
}
```



