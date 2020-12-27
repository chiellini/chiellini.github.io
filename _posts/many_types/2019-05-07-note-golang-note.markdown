---
title: "GOLANG 编程基础"
subtitle: "golang programming base "
layout: post
author: "lizelin"
header-style: text
catalog: true
tags:
  - 软件基础
  - Golang
  - Programming
  - 笔记
---
# go 的基本情况

## 用途

Go 语言被设计成一门应用于搭载 Web 服务器，存储集群或类似用途的巨型中央服务器的系统编程语言。

对于高性能分布式系统领域而言，Go 语言无疑比大多数其它语言有着更高的开发效率。它提供了海量并行的支持，这对于游戏服务端的开发而言是再好不过了。

## 语言结构

* package main 定义包名，必须在源文件中非注释的第一行指明这个文件属于哪一个包。package main表示可独立执行的程序，每个go都包含一个名为main的包。

* import  "fmt"表示 告诉go编译器这个程序需要使用fmt包（函数或者其他元素），fmt实现包括了格式化IO的函数

  ```go
  import (
     "fmt"
     "math"
  )
  ```

  

* main 函数是每一个可执行程序所必须包含的，一般来说都是在启动后第一个执行的函数（如果有 init() 函数则会先执行该函数）

* fmt有Print和Println两个，第二个会换行。

* 关于公有私有。当一个（常量，变量，类型，函数名，结构字段）以大写字母开头时候，那么它就是导出（公有，public);如果是首字母小写，那就是私有的，对包外不可见。


## 数据类型

* bool型  

  * ```
    var b bool = true
    ```

* 数字类型

  * int, float32, float64, complex

  * 

  * | 1    | **uint8** 无符号 8 位整型 (0 到 255)                         |
    | ---- | ------------------------------------------------------------ |
    | 2    | **uint16** 无符号 16 位整型 (0 到 65535)                     |
    | 3    | **uint32** 无符号 32 位整型 (0 到 4294967295)                |
    | 4    | **uint64** 无符号 64 位整型 (0 到 18446744073709551615)      |
    | 5    | **int8** 有符号 8 位整型 (-128 到 127)                       |
    | 6    | **int16** 有符号 16 位整型 (-32768 到 32767)                 |
    | 7    | **int32** 有符号 32 位整型 (-2147483648 到 2147483647)       |
    | 8    | **int64** 有符号 64 位整型 (-9223372036854775808 到 9223372036854775807) |

  * 

    

  * | 序号 | 类型和描述                        |
    | :--- | :-------------------------------- |
    | 1    | **float32** IEEE-754 32位浮点型数 |
    | 2    | **float64** IEEE-754 64位浮点型数 |
    | 3    | **complex64** 32 位实数和虚数     |
    | 4    | **complex128** 64 位实数和虚数    |

    | 1    | **byte** 类似 uint8                      |
    | ---- | ---------------------------------------- |
    | 2    | **rune** 类似 int32                      |
    | 3    | **uint** 32 或 64 位                     |
    | 4    | **int** 与 uint 一样大小                 |
    | 5    | **uintptr** 无符号整型，用于存放一个指针 |

* 字符串类型

  * Go 语言的字符串的字节使用 UTF-8 编码标识 Unicode 文本。

* 派生类型

  * 指针（Pointer)
  * 数组
  * 结构化类型
  * Channel类型
  * 函数类型
  * 切片类型
  * 接口类型(interface)
  * Map类型

### 变量

* var identifier type

  * 如果没有初始化，默认为零

* 以下几种类型空的时候为 nil

  * ```go
    var a *int
    var a []int
    var a map[string] int
    var a chan int
    var a func(string) int
    var a error // error 是接口
    ```

* ```go
  package main
  
  var x, y int
  var (  // 这种因式分解关键字的写法一般用于声明全局变量
      a int
      b bool
  )
  
  var c, d int = 1, 2
  var e, f = 123, "hello"
  
  func main(){
      //这种不带声明格式的只能在函数体中出现
      //g, h := 123, "hello"
      g, h := 123, "hello" //:=左边的变量一定要未声明的
      println(x, y, a, b, c, d, e, f, g, h)
  }
  ```

#### 值类型和引用类型

* 像int,float, bool , string 这些基本类型都是属于值类型
  * 使用这些类型的变量直接指向内存中的值。这几个类型如果将一个变量的值复制给另一个变量的时候，实际上是把值进行了拷贝而已。
* &i可以获取i的内存地址。值类型的变量的值储存在**栈**之中。
  * 除了基本类型的变量，更加复杂的数据通常会需要使用多个字，这些数据一般使用引用类型保存。
  * 一个引用类型的变量r1储存的是r1所在的内存地址，或者内存地址中第一个字坐在的位置。
* 这个内存地址被称为指针，这个指针实际上也被存储在另外的某一个字中。
  * 同一个引用类型的多个指针指向的多个字可以是连续的内存地址中，计算效率最高。
  * 如果这些字分散存放在内存中，每一个字都知识了下一个字所在的内存地址。

#### 变量声明

* a:=1  编译器会自动根据后面的值来生成a的类型，这里就是int

* 在函数里面声明的变量必须被使用，否则会报错：a declared and not used

* 全局变量可以允许声明但是不使用。

* 交换两个变量的值（类型相同）

  * 
    如果你想要交换两个变量的值，则可以简单地使用 a, b = b, a，两个变量的类型必须是相同。


  * 空白标识符 _ 也被用于抛弃值，如值 5 在：_, b = 5, 7 中被抛弃。(临时变量)

    _ 实际上是一个只写变量，你不能得到它的值。这样做是因为 Go 语言中你必须使用所有被声明的变量，但有时你并不需要使用从一个函数得到的所有返回值。

#### 变量作用域

* 函数内定义的变量称为局部变量
  * 简单易懂，不解释
* 函数外定义的变量称为全局变量
  * 简单易懂，不解释
* 函数定义中的变量称为形式参数
  * 绝了，就是函数的形式参数，简称形参

### 常量

const identifier [type] = value

type 可以省略，会根据后面的value来赋予类型。

* 常量可以用作枚举

  * ```go
    const (
        Unknown = 0
        Female = 1
        Male = 2
    )
    ```

* 常量可以用内置函数 len(), cap(), unsafe.Sizeof()来进行赋值

  * ```go
    package main
    
    import "unsafe"
    const (
        a = "abc"
        b = len(a)
        c = unsafe.Sizeof(a)
    )
    
    func main(){
        println(a, b, c)
    }
    ```

#### iota

可以被编译器修改的常量。

* iota 在 const关键字出现时将被重置为 0(const 内部的第一行之前)，const 中每新增一行常量声明将使 iota 计数一次(iota 可理解为 const 语句块中的行索引)。

* ```go
  package main
  
  import "fmt"
  
  func main() {
      const (
              a = iota   //0
              b          //1
              c          //2
              d = "ha"   //独立值，iota += 1
              e          //"ha"   iota += 1
              f = 100    //iota +=1
              g          //100  iota +=1
              h = iota   //7,恢复计数
              i          //8
      )
      fmt.Println(a,b,c,d,e,f,g,h,i)
  }
  ```

* iota 表示从 0 开始自动加 1，所以 **i=1<<0**, **j=3<<1**（**<<** 表示左移的意思），即：i=1, j=6，这没问题，关键在 k 和 l，从输出结果看 **k=3<<2**，**l=3<<3**。

  简单表述:

  - i=1

  - ：左移 0 位,不变仍为 1;

  - **j=3**：左移 1 位,变为二进制 110, 即 6;
  - **k=3**：左移 2 位,变为二进制 1100, 即 12;
  - **l=3**：左移 3 位,变为二进制 11000,即 24。

* ```go
  package main
  
  import "fmt"
  const (
      i=1<<iota
      j=3<<iota
      k
      l
  )
  
  func main() {
      fmt.Println("i=",i) //1
      fmt.Println("j=",j) //6
      fmt.Println("k=",k) //12
      fmt.Println("l=",l) //24
  }
  ```

### 运算符

* 算术运算符 加减乘除，求余，自增++，自减--

* 关系运算符 大鱼小鱼等

* 逻辑运算符

  * && 
  * ||
  * ！

* 位运算符

  * & 与运算
  * | 或运算
  * ^ 异或运算

* 赋值运算符

* 

  * | <<=  | 左移后赋值     | C <<= 2 等于 C = C << 2 |
    | ---- | -------------- | ----------------------- |
    | >>=  | 右移后赋值     | C >>= 2 等于 C = C >> 2 |
    | &=   | 按位与后赋值   | C &= 2 等于 C = C & 2   |
    | ^=   | 按位异或后赋值 | C ^= 2 等于 C = C ^ 2   |
    | \|=  | 按位或后赋值   | C \|= 2 等于 C = C \| 2 |

### 语言接口(未实现的方法)

go语言提供了另外一种数据类型--接口，它把所有具有共性的方法定义在一起，任何其他类型只要实现了这些方法就是实现了这个接口。

接口的定义和类中函数定义一样，不是（go没有类）在结构体里面定义，而是在外面，把结构体当做的一个接受者，把函数定义好了给他。

```go
package main
import (
    "fmt"
)
type Phone interface {//接口，虚类父类什么的
    call()
}
type NokiaPhone struct {//具体实现的类，子类什么的
}

func (nokiaPhone NokiaPhone) call() {
    fmt.Println("I am Nokia, I can call you!")
}

func main() {
    var phone Phone
    phone = new(NokiaPhone)
    phone.call()
}
```



## 基本语法

* 标记：关键字，标识符，常量，字符串，符号

* 一行一条语句，像python(鼓励这样)

### 标记

* 标识符

  * 标识符用力啊命名变量、类型等程序实体。

* 关键字（保留字）

  * 25个关键字

    

  * | break    | default     | func   | interface | select |
    | -------- | ----------- | ------ | --------- | ------ |
    | case     | defer       | go     | map       | struct |
    | chan     | else        | goto   | package   | switch |
    | const    | fallthrough | if     | range     | type   |
    | continue | for         | import | return    | var    |

  * 36个预定义标识符

    

  * | append | bool    | byte    | cap     | close  | complex | complex64 | complex128 | uint16  |
    | ------ | ------- | ------- | ------- | ------ | ------- | --------- | ---------- | ------- |
    | copy   | false   | float32 | float64 | imag   | int     | int8      | int16      | uint32  |
    | int32  | int64   | iota    | len     | make   | new     | nil       | panic      | uint64  |
    | print  | println | real    | recover | string | true    | uint      | uint8      | uintptr |

* 空格

  * ```go
    var age int;
    ```

### 条件语句

* switch

  * ```go
    switch var1 {
        case val1:
            ...
        case val2:
            ...
        default:
            ...
    }
    ```

* select  select 是 Go 中的一个控制结构，类似于用于通信的 switch 语句。每个 case 必须是一个通信操作，要么是发送要么是接收。

  select 随机执行一个可运行的 case。如果没有 case 可运行，它将阻塞，直到有 case 可运行。一个默认的子句应该总是可运行的。

* if var<20{

  }

### 循环语句

* for语句和C语言一样，只不过不要括号

  * for {}   相当于C语言的for(;;)

  * for 循环的 range 格式可以对 slice、map、数组、字符串等进行迭代循环。格式如下：(和python一样。)

  * ```
    for key, value := range oldMap {
        newMap[key] = value
    }
    ```

### 语言函数

Go 语言函数定义格式如下：

* ```
  func function_name( [parameter list] ) [return_types] {
     函数体
  }
  ```

Go 函数可以返回多个值，例如：

* ```
  package main
  
  import "fmt"
  
  func swap(x, y string) (string, string) {
     return y, x
  }
  
  func main() {
     a, b := swap("Mahesh", "Kumar")
     fmt.Println(a, b)
  }
  ```

引用传递

* ```go
  /* 定义交换值函数*/
  func swap(x *int, y *int) {
     var temp int
     temp = *x    /* 保持 x 地址上的值 */
     *x = *y      /* 将 y 值赋给 x */
     *y = temp    /* 将 temp 值赋给 y */
  }
  ```

  使用的时候就把&i作为参数传进去。

####函数变量（像js一样便捷的定义函数）

```go
package main

import (
   "fmt"
   "math"
)

func main(){
   /* 声明函数变量 */
   getSquareRoot := func(x float64) float64 {
      return math.Sqrt(x)
   }

   /* 使用函数 */
   fmt.Println(getSquareRoot(9))

}
```

#### 闭包

匿名函数，闭包。

里面的变量是通用的，只要是这个函数，那么他就还是那一个变量。

#### 方法(类（结构体中的函数))

一个方法就是一个包含了接受者的函数。接受者可以是命名类型或者结构体类型的一个值/指针。

方法相当于是对象里面的一个实例函数。

Go 没有面向对象，而我们知道常见的 Java、C++ 等语言中，实现类的方法做法都是编译器隐式的给函数加一个 this 指针，而在 Go 里，这个 this 指针需要明确的申明出来，其实和其它 OO 语言并没有很大的区别。

在 C++ 中是这样的:

```
class Circle {
  public:
    float getArea() {
       return 3.14 * radius * radius;
    }
  private:
    float radius;
}

// 其中 getArea 经过编译器处理大致变为
float getArea(Circle *const c) {
  ...
}
```

在 Go 中则是如下:

```go
type Circle struct {
    radius float64
}

func (c Circle) getArea() float64 {
 	//c.radius 即为 Circle 类型对象中的属性
    //可以在函数里设置初始值
    c.radius=10
 	return 3.14 * c.radius * c.radius
}

func main() {
	var c1 Circle
	c1.radius=10
    fmt.Println("圆的面积",c1.getArea())
}
```

### 数组

数组是具有相同唯一类型的一组已编号且长度固定的数据项序列。

```go
var variable_name [SIZE] variable_type
```

* 初始化数组

    * ```go
      var balance = [5]float64{1000,2,3,5,6}

      var balance =[…]float32{1,2,3,4,5,6} //会根据后面的动态分配

      balance[4] = 50.0    //没有设置大小，但是长度还是是5
      ```

* 访问数据，多维数组。

* 用数组作为形参。

  * 方法一，形参设定数组大小
    ```go
    void myFunction(param [10]int)
    {
    .
    .
    .
    }
    ```

  * 方法二，形参不设定数组大小

    ```go
    void myFunction(param []int)
    {
    .
    .
    .
    }
    ```

### 指针

指针的定义和C语言相似，

* ```go
  var ip *int        /* 声明指针变量 */
  ```

* 空指针==nil

#### 指针数组

```go
var ptr [MAX]*int
for i=0;i<MAX;i++ {
    ptr[i]=&a[i]
}
for i=0;i<MAX;i++ {
    fmt.Prinf("a[%d] = %d\n", i,*ptr[i])
}
```

#### 双重指针

```go
var ptr **int
```

#### 指针参数

````go
func swap(x *int,y *int){
    var temp int
    temp = * x
    *x=*y
    *y=temp
}
````

### 结构体

```go
type struct_variable_type struct {
    member definition
    ...
}

type Books struct {
    title string
    author string
    subject string
    book_id int
}

//直接创建结构体
fmt.Println(Books{"string1","string2","string3",1314})
//创建的时候也可以采用键值对的方法
fmt.Println(Books{title:"string1",author:"string2",subject:"string3",book_id:1314})
//访问成员，和C语言一样，
book.title
```

结构体作为形参，和C语言一样，只不过不用加struct

```
func printBook( book Books){
    
}
```

#### 结构体指针

```go
var struct_pointer *Books
struct_pointer = &Book1
struct_pointer.title
```

### 切片

切片的定义

* 长度

```go
//第一种方式
var identifier []type
//第二种方式
var slice1 []type = make([]type,len,<capability>)
//可以简写
slice1 :=make([]type,len,<capability>)
// 切片是可以索引的，len()可以获取
// 切片提供了计算容量的方法cap(),可以测量切片最长可以切多长
```

如果想增加切片的容量，我们必须创建一个更大的切片并把原来的内容都拷贝过来。

```go
//copy()和append()
//允许追加空切片
numbers=append(numbers,0)
/* 创建切片 numbers1 是之前切片的两倍容量*/
numbers1 := make([]int, len(numbers)，(cap(numbers))*2)

/* 拷贝 numbers 的内容到 numbers1 */
copy(numbers1,numbers)
 
```

### range

相当于python里面的enumerate

```go
nums := []int{2, 3, 4}
    sum := 0
    for _, num := range nums {
        sum += num
    }
    fmt.Println("sum:", sum)
    //在数组上使用range将传入index和值两个变量。上面那个例子我们不需要使用该元素的序号，所以我们使用空白符"_"省略了。有时侯我们确实需要知道它的索引。
    for i, num := range nums {
        if num == 3 {
            fmt.Println("index:", i)
        }
    }
    //range也可以用在map的键值对上。
    kvs := map[string]string{"a": "apple", "b": "banana"}
    for k, v := range kvs {
        fmt.Printf("%s -> %s\n", k, v)
    }
    //range也可以用来枚举Unicode字符串。第一个参数是字符的索引，第二个是字符（Unicode的值）本身。
    for i, c := range "go" {
        fmt.Println(i, c)
    }
}
```

### Map（集合）

```go
var map_variable map[key_data_type]value_data_type
//或者
map_variable := make(map[key_data_type]value_data_type)
```

#### delete()函数

```go
dele(map_varibale,key_name)
```

## go的错误处理

go语言内部有一个错误接口error,这是一个接口类型，定义如下

```go
type error interface {
    Error() string
}
```

在编码中，通过实现error接口类型来生成错误信息

函数通常在最后的返回值中返回错误信息，使用errors.New

```go
func Sqrt(f float64)(float64,error) {
    if f<0 {
        return 0,errors.New("math:square root of negative number")
    }
}

result,err:=Sqrt(-1)

if err!=nil {
    fmt.Prinln(err)
}
```

## go并发

### goroutine

go语言支持并发，我们只需要通过go关键字来开启goroutine即可。

goroutine是轻量级线程，goroutine的调度是由golang运行时进行管理的。

```go
go func_name(...)
//Go允许使用go语言开启一个新的运行期线程，goroutine，就是用一个不同的，新创建的goroutine来执行一个函数。
```

### channel

通道是用来传递数据的一个数据结构。

通道可以用于两个goroutine之间通过传递一个指定类型的值来同步运行和通讯。操作符 <- 用来指定通道方向，发送或者接受。如果没有指定方向，则为双向通道。

```go
ch <- v //把v发送到通道ch
v := <- ch //从ch接受数据
			//并把值付给y
```

注意：默认情况下，通道是不带缓冲区。所以发送端在发送数据的时候，接收端要同事接受相应的数据。

```go
package main
import "fmt"
func sum(s []int, c chan int) {
    sum := 0
    for _, v := range s{
        sum+=v
    }
    c <- sum //把相加结果发到通道c
}

func main() {
    s:=[]int{1,2,3,4,5,6,7}
    
    c:=make(chan int)
    go sum(s[:len(s)/2],c)
    go sum(s[len(s)/2:],c)
    x,y:= <-c,<-c //取出
    //这个语句相当于实时等待通道中的数据吧
    //立马读出
}
```

###通道缓冲区

可以设置缓冲区，后面是缓冲区大小

```go
ch := make(chan int,2)
ch <- 1
ch <- 2
fmt.Println(<-ch)
fmt.Println(<-ch)
```



### go遍历和关闭通道

```go
v,status := <-ch
```

通道关闭的实例

```go
package main
import "fmt"
func fibonacci(n int,c chan int) {
    x,y:=0,1
    for i:=0;i<n;i++{
        c<-x
        x,y=y,x+y
    }
    close(c) //这相当于内置函数，如果检测到status的
}

func main(){
    c:=make(chan int,10)
    go fibonacci(cap(c),c)
	   
	fmt.Println(len(c))
    for  z:=0;z<10+10;z++ {
		value,status:= <-c
		fmt.Println(value)
		fmt.Println(status)
    }
}
```



 