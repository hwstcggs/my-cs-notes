# GOOS：目标平台的操作系统（darwin、freebsd、linux、windows） GOARCH：目标平台的体系架构（386、amd64、arm）



**Mac 下编译 Linux 和 Windows 64位可执行程序：**

```
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build
```

####  {#linux-下编译-mac-和-windows-64位可执行程序：}

#### Linux 下编译 Mac 和 Windows 64位可执行程序： {#linux-下编译-mac-和-windows-64位可执行程序：}

```
CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build
```

####  {#windows-下编译-mac-和-linux-64位可执行程序：}

#### Windows 下编译 Mac 和 Linux 64位可执行程序： {#windows-下编译-mac-和-linux-64位可执行程序：}

```
CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build
```



