# go语言学习基础
## 环境配置
+ 安装和配置SDK [go安装包网站]（https://studygolang.com/dl）
+ 设置环境变量`GOPATH`为go的SDK安装目录
## 变量和数据类型
### 变量的声明和赋值
```GO
package main
import "fmt"

func main(){
    // 第一种方式声明和赋值
    var age1 int = 18

    // 第二种指定默认类型，不赋值，使用默认值
    var age2 int  //默认为0

    // 第三种不指定类型，根据=后面的值进行类型判定
    var age2 = 18

    // 第四种省略 var 和类型
    age2:=18
}
```
同时GO支持多个变量的声明
```GO
func main(){
    var n1, n2, n3 int

    var n4, name, n5 = 10, "jack", 7.8

    n6, height := 6.9, 100
}
```
## 变量的数据类型分类
+ 基本数据类型
    + 数值型
        + 整数类型（int，int8，int16，int32，int64, uint8,....byte)
        + 浮点类型 (float32, float64)
    + 字符型 (没有单独的字符型，使用byte来保存单个字母字符)
    + 布尔型 (bool)
    + 字符串型 (string)
+ 派生/复杂数据类型
    + 指针
    + 数组
    + 结构体
    + 管道
    + 函数
    + 切片
    + 接口
    + map
## 数组
### 数组定义格式
`var 数组名 [数组大小]数据类型`
### 数组的遍历
+ 普通for循环
+ `for key, val := range 数组 {...}`
### 数组初始化
+ `var arr1 3[int] = [3]int{3, 6, 9}`
+ `var arr2 = [3]int{1, 4, 7}`
+ `var arr3 = [...]int{4, 5, 6}`
+ `var arr4 = [...]int{2:66, 1:99, 3:88}`
### 数组注意事项
+ 数组的长度是类型的一部分
+ 数组函数传参数也是值传递
+ 如果在其他函数中，去修改原来的数组，需要传指针
## 切片
切片是对数组一个连续片段的引用，本质是一个结构体，依次存放底层数组的指针，切片的长度和切片的容量
### 切片的定义
```GO
package main(){
    // 使用切片去引用一个已创建的数组
    var arr [4]int = [4]int{1, 2, 3, 4}
    slice := arr[1:2]

    //make函数三个参数，切片类型，切片长度，切片容量
    slice := make([]int, 4, 20)
}
```
### 切片的动态增长
```GO
func main(){
    var arr [6]int = [6]int{1, 2, 3}
    var slice []int = arr[1:4]
    
    //创建一个新数组，将原来数组中的数值拷贝到新数组中，在新数组中追加扩容
    slice2 := append(slice, 88, 50)
    slice := append(slice2, slice...)
}
```
## map
### map的创建
```GO
import "fmt"
func main(){
    //定义map变量
    var a map[int]string  //声明map，但是没有分配空间
    a = make(map[int]string, 10) 

    //采用{}
    c := map[int]string{
        2012: "张三",
        2013: "李四"
    }
}
```
+ 增加修改 `map[key] = value`
+ 删除 `delete(map, key)`,如果`key`存在，就删除该`key-value`, 如果不存在，不操作，也不报错
+ 清空操作，没有一个专门的方法一次删除，可以遍历一下`key`，逐个删除；或者`map = make(...), make一个新的，让原来的成为垃圾，被gc回收
+ 查找操作:
`value, bool = map[key]`, 其中`value`为返回的`value`，`bool`为返回的值是否存在，要么`true`，要么`false`
## 运算符
+ 算术运算符 `+、-、*、/、%、++、--`
+ 赋值运算符 `+、 +=、 -=、 *、 /=、 %=`
+ 关系运算符 `<=、>=、==`
+ 逻辑运算符 `&&、||、！`
+ 位运算符   `&、|、^`
+ 其他运算符 ‵& 取地址、* 取地址里的值
## 流程控制语句
### 条件分支
#### if 条件分支
```GO
func main(){
    // 注意条件中的()可以省略， {}一定不可以省略
    if (条件表达式){

    }else if{      //else if 和else只能写在这一行

    }else{

    }
}
```
#### switch多分支
```GO
func main{
    var socre int = 87
    // default 可以放在任意位置
    // 可以不用写break
    // switch穿透，利用fallthrough关键字，case语句增加fallthrough后，则会执行下一个case，也叫switch穿透
    switch score/10 {
        case 10 : 
        case 9 :
        ...
        default:

    }
}
```
## 循环语句
只有`for`循环，没有`while`和`do...while`
```GO
func main(){
    // for 初始表达式; 布尔表达式; 迭代因子{
    //    循环体
    // }
    sum := 0
    //注意: for 的初始表达式，不能用var定义变量形式
    for i := 1; i <= 5; ++i{
        sum += i
    }
}
```
## 函数
### 函数命名要求
+ 遵循驼峰命名规范
+ 首字母不能是数字
+ 首字母大写该函数可以被本包文件和其他包文件使用
+ 首字母小写该函数只能被本包文件使用
### 返回值
+ 返回值可以0～n个
+ 返回值一个的话，那么()可以省略不写
### 其他注意事项
+ go不支持函数重载
+ 对于基本类型和数组，go以值的形式传递
+ go的参数支持可变参数, 例如(args... int)可以传入任意数量的int类型, 可用
```GO
// func 函数名(形参列表)(返回值类型列表){
//  执行语句...
//  return + 返回值列表    
//}
func test (args...int){
    for i := 0; i < len(args); ++i{
        fmt.Println(args[i])
    }
}
```
+ 函数也是一种数据类型，可以作为新参
+ 支持type起别名定义数据类型, 例如`type myFunc func(int, int)(int)`
+ 支持对返回值命名
```GO
func test(num1 int, num2 int)(sum int, sub int){
    sum := num1 + num2
    sub := num1 - num2
    return sum, sub
}
```
## 包的引入
+ `import`导入语句通常放在文件开头包声明语句下面，包名从`$GOPATH/src`后开始计算的，使用`/`进行路径分隔
+ main包是程序入口包，一般`main`函数会放在这个`main`包下，否则不能编译执行
+ 包声明的名字可以和文件夹、文件名不一样
+ 同一个目录下的同级文件归属于一个包，包的声明的名称必须一致 
## 错误处理机制
### defer+recovery机制
```GO
import "fmt"
func add(num1 int, num2 int) int{
    // 在Golang中，程序遇到defer关键字，不会立即执行defer后的语句，而是将defer后的语句压入一个栈中，而是函数执行好后，在将语句出栈
    defer fmt.Println("num1=", num1)
    defer fmt.Println("num2=", num2)
}
```
内建函数recover允许程序管理恐慌个过程中的GO程序，在defer函数中，执行recover调用会取回传至panic调用的错误值，恢复正常运行，停止恐慌过程，若recover在defer函数之外被调用，它将不会停止恐慌过程序列，在此情形下，当Go程序处在不在恐慌的过程中，或者提供给panic的实参为`nil`时，`recover`就会返回`nil`
### 自定义错误类型
需要调用`errors`包下的`New`函数
```GO
import(
    "fmt"
    "errors"
)
func test()(err error){
    num1 := 10
    num2 := 0
    if num2 == 0{
        return errors.New("除数为0")
    }else{
        result := num1 / num2
        return nil
    }
}
func main(){
    err := test()
    panic(err)  //可以借助`builtin`包下内置函数`panic`终止程序
}
```
## 面向对象编程
+ Golang没有类（class）， Go的结构体（struct）和其他编程语言的类具有同等地位的
+ 去掉OOP语言的函数重载，构造函数和析构函数、隐藏的this指针等
+ Go仍然有面向对象编程的继承、封装和多态的特性
### 结构体封装
```Go
type Teacher struct{
    //变量名大写，为公有属性，外界可以访问该变量
    Name string
    Age int
    School string
}
func main(){
    var t Teacher = Teacher{}

    var t *Teacher = new(Teacher)
}
```
### 方法的定义
+ 结构体是值类型，方法采用值传递的形式，需要改变需要传递指针
```Go
func (p Person) test(){
}
func (p *Person) test2(){
    p.Name = "luna"
}
func main(){
    var p Person
    p.Name = "lulu"
    p.test()     
    p.test2()
}
```
### 继承
+ GO采用嵌入匿名结构体的方式，实现继承
+ 结构体可以使用嵌套匿名集结构体中所有字段和方法
+ 如果结构体嵌入两个匿名结构体，如果两个匿名结构体有相同的字段和方法时，在访问时，就必须明确指明匿名结构体名字
+ 如果结构体中嵌入了一个有名的结构体，则为组合
```GO
type Student struct{
    Name string
    Age int
    Score int
}

func (stu *Student) ShowInfo{
    fmt.Printf("Student name = %v\n", stu.Name)
}

type Pupil struct{
    Student 
}

func main(){
    graduate := &Pupil{}
    //采用如下方式调用继承类中的方法， 也可以省略匿名结构体字段访问
    graduate.Student.Name = "tom"
    graduate.Student.showInfo() 
}
```
### 接口
+ 接口不能写实现，且不能包含任何变量
+ 接口不能创建实例，但是可以指向一个创建接口的实例
+ 自定义类型就可以实现接口，不需要一定是结构体类型
+ 接口可以继承其他接口，实现必须实现所有的接口方法 
```GO
// 声明/定义一个接口
type Usb interface{
     Start()
     Stop()
}

type Phone struct{
}

// 让Phone 实现Usb接口的方法
func (p Phone) start(){
    fmt.Println("手机开始工作...")
}
func (p Phone) Stop(){
    fmt.Println("手机停止工作...")
}

// 让Phone 实现Usb接口的方法
func (c Camera) start(){
    fmt.Println("手机开始工作...")
}
func (c Camera) Stop(){
    fmt.Println("手机停止工作...")
}

type Computer struct{
}

// 编写一个方法working，接受一个usb接口类型变量
// 只要实现了Usb接口（实现了Usb接口声明所有方法），就能传给接口类型的形参
func (c Computer) Working(usb Usb){
    usb.Start()
    usb.Stop()
}

func main(){

}
```
## 协程
### GO协程的特点
+ 有独立的栈空间
+ 共享程序堆空间
+ 调度由用户控制
+ 协程是轻量级线程，逻辑态，可以容易起上万个
```GO
package main
import(
    "fmt"
    "strcoonv"
    "time"
)
func test(){
    for i := 1; i < 10; i++{
        fmt.Println("test() hello world" + strcon.Itoa(i))
        time.Sleep(time.Second)
    }
}
func main(){
  
    go test()  //开启一个协程

    //主线程退出了，即使协程没有执行完，也会退出
    for i := 1; i < 10; i++{
        fmt.Println("main() hello" + strcon.Itoa(i))
        time.Sleep(time.Second)
    }
} 
```
### goroutine的调度模型
#### MPG模式基本介绍
+ M：操作系统的主线程（物理线程）
+ P：协程执行的上下文
+ G：协程，可以构成一个队列
### 资源竞争的解决办法
+ `go build`添加 `-race`参数可以检查程序的竞争现象
#### 互斥锁
通过加锁解决程序竞争现象
```GO
import(
    "fmt"
    "sync"
)
var (
    myMap = make(map[int]int, 10)
    lock sync.Mutex
)
func test(n int){
    res := 1
    for i := 1; i < n; i++{
        res *= i
    }

    lock.Lock()
    myMap[n] = res
    lock.Unlock()
}
```
## 管道
### 管道的基本使用
+ 管道可以认为是一个线程安全的消息队列
+ 管道必须是引用类型，必须初始化才能写入数据，即make后才能使用
+ 往管道中添加数据时，不能超过其容量
+ 管道的声明 `var 变量名 chan 数据类型`
```GO
func main(){
     var intChan chan int
     intChan  = make(chan int, 3)

     //向管道写入数据
     intChan<- 10
     num := 211
     intChan<- num

     //从管道中读取数据
     var num2 int
     num2 = <-intChan
}
```
+ 管道关闭后，就不能再向`channel`里写数据了，但是仍然可以从中读取数据
+ 管道支持`for-range`的方式遍历，管道未关闭就遍历会出现`deadlock`
```GO
func main(){
    intChan := make(chan int, 3)
    intChan<- 100
    intChan<- 50
    close(intChan)

    for v := range intChan{
        fmt.Println("v=", v)
    }
}
```
### 管道的使用注意事项
+ 管道可以声明成只读`var chan3 <-chan int`，可以在函数参数中声明防止在被调用函数中写管道
+ 也可以声明成只写`var chan3 chan<- int`
+ 使用`select`可以解决数据阻塞现象
```GO
func main(){
    intChan := make(chan int, 10)
    strChan := make(chan string, 5) 

    for {
        select {
            //如果intChan一直没有关闭，不会一直阻塞而deadlock, 会自动匹配到下一个case
            case v := <-intChan :
                fmt.Printf("从intChan中读取数据%d\n", v)
            case v := <-strChan :
                fmt.Printf("从strChan中读取数据%d\n", v)
        }
    }
}
```
+ `goroutine`中使用`defer + recover`，可以解决程序中出现`panic`导致程序崩溃现象
## 反射
```GO
func test(){
    defer func(){
        if err := recover(); err ！= nil{
            fmt.Println("test() 发生错误", err)
        }
    }()
}
```
## 反射
+ 在运行时动态获取变量各种信息，比如变量的类型、类别
+ 如果是结构体变量，还可以获取结构体本身的信息（包括结构体的字段、方法）
+ 通过反射，可以修改变量的值，还可以调用关联的方法
+ 不知道接口调用哪个函数，根据传入参数在运行时确定调用的具体接口
`fucn bridge(funcPtr interface{}, args ...interface{})` 
### 反射的重要函数
`reflect.TypeOf(变量名)`, 获取变量的类型，返回`reflect.Type`类型
`reflect.ValueOf(变量名)`， 返回`reflect.Value`类型, 是一个结构体类型
+ 变量、`interface{}`和`reflect.Value`可以相互转换
```GO
// 变量<--->interface{}<--->reflect.Value
type Student struct{

}

func test(b interface{}){
    // interface{}转成 reflect.Value
    rVal := reflect.ValueOf(b)

    // reflect.Value -> interface{}
    iVal = rVal.Interface{}
    
    //使用类型断言将interface{}转换化为原来变量
    v := iVal(Student)
}
```
