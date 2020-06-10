# go学习笔记

# 数组

## 数组全等比较

长度是数组类型的一部分,相同类型的数组可以比较

```go
a := [...]int{1,2}
//b := [...]int{1,2,3}   a==b panic
c := [...]int{2,1}
d := [...]int{1,2}
fmt.Println(a==c,a==d)  //false true
```



# 切片

## 全等比较

[]byte切片可以使用bytes.Equal进行深度比较,但是对于其他类型的slice，我们必须自己展开每个元素进行比较

```go
a := []byte{1,2}
b := []byte{1,2,3}
fmt.Println(bytes.Equal(a,b))  //false
```

比较好的操作是禁止slice之间的比较操作,

slice可以和nil进行比较  `if s==nil { }`可以判断slice是否经过初始化,

判断slice是否为空应该用  `len(s)==0` 

```go
var s []int           // len(s) == 0, s == nil
fmt.Println(s==nil)       // true
s = nil             // len(s) == 0, s == nil
s = []int(nil)           // len(s) == 0, s == nil
fmt.Println(s==nil)       // true
s = []int{}          // len(s) == 0, s != nil
fmt.Println(s==nil)        // false
```





# package

## 导入包

自定义包名一般和目录名保持一致

同一目录下的包名保持一致

导入自定义包时从 ```$GOPATH/src``` 路径开始

例:自定义mode包

![image-20200604175911270](../static/images/image-20200604175911270.png)

导入时 ``` import "awesomeProject/mode" ```  ($GOPATH=E:\tongyan\code\go\src)

## 遇到的问题

### import 显示  cannot resolve directory

解决:原因是Goland 编辑器中项目设置为 go modules 项目，导致从gomod读取，从而飘红，具体修改设置如下：将此处的对号删除
![image-20200604180726602](../static/images/image-20200604180726602.png)

### package awesomeProject/mode is not in GOROOT (E:\tongyan\program\go\src\awesomeProject\mode)

解决: 将 [GO111MODULE](#GO111MODULE ) 设置为 off  (cmd执行```go env -w GO111MODULE=off```)



# 参数

## GO111MODULE

用环境变量 `GO111MODULE` 开启或关闭模块支持，它有三个可选值：`off`、`on`、`auto`，默认值是 `auto`。

- `GO111MODULE=off` 无模块支持，go 会从 GOPATH 和 vendor 文件夹寻找包。
- `GO111MODULE=on` 模块支持，go 会忽略 GOPATH 和 vendor 文件夹，只根据 `go.mod` 下载依赖。
- `GO111MODULE=auto` 在 `$GOPATH/src` 外面且根目录有 `go.mod` 文件时，开启模块支持。

在使用模块的时候，`GOPATH` 是无意义的，不过它还是会把下载的依赖储存在 `$GOPATH/src/mod` 中，也会把 `go install` 的结果放在 `$GOPATH/bin` 中。











