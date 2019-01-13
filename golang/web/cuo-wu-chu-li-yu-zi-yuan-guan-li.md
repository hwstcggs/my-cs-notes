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



