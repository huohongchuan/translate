# 欢迎新的Gopher

本章的目的是为了让您从宏观方面了解Go的基础知识。在我们学习Go的**工具链**、**语法**和**类型**系统之前，我们将会在不同操作系统平台下安装Go，写下第一份Go代码作为起步。让我们开始吧。

## 安装

写Go代码的第一步就是着手安装Go语言，你可以访问[https://golang.org/doc/install](https://golang.org/doc/install) Go的开发者为Windows，Mac OS和Linunx都提供了安装包。当然，如果您的系统并提供安装程序，您也可以使用go的源码安装。

一旦安装完毕go之后，在命令行下输入`go version`，终端将会打印所安装的go的版本。如果发生错误，重启命令行重新输入，否则可能需要像go的[官网](https://golang.org/)报告错误并寻求解决办法。

> Go的别名golang
> 
> Go 的官网是 [golang.org](https://golang.org/)，语言的全面其实是“golang”。当您使用“Go”关键字搜索的时候找不到解决问题有效的办法，可以尝试搜索关键字“Golang”。他们两者本质上是等价的


### Go工作区（Workspace）

通过本书，你将会感知到Go是一门强制选择配置的语言，你必须按照Go的方式构建工作区和组织代码。其他语言你可以根据自己下喜好任意组织代码，Go则希望你使用Go的方式，将你的所有项目源码存放一个特殊路径`GOPATH`的文件夹中。这样做的好处是你可以轻松的是用go工具下载和管理第三方（third-party）包源码，如果不这样做，除了标准库之外，你将无法使用任何第三方包。

这很可能与你熟悉的工作方式不同，请尽量尝试改变吧。起初我也很反感，后来尝试学习并接受Go的方式（Go way），如今已经习惯这样的代码管理方式。

`GOPATH`路径中可以有多个子文件夹，最重要的一个莫过于`src`文件夹。src文件夹存放你写的go代码和go的第三方包源码。现在创建一个文件命名为`src`。当你开始写go代码的时候，请将这些代码保存在src文件夹中。为了告诉Go哪一个文件夹为`GOPATH`路径，我们需要设置一个同名的环境变量（environment variables）。如果你对环境变量不熟，下面将会逐一接受在在Windows，Mac OS, Linux不同系统中的配置。

#### Mac OS 和 Linux

每当命令行窗口启动的时候，都会加载一个`bash profile`的文件，
在Mac OS 和 Linux中设置环境变量，只需要往这个bash中添加即可：

```
echo "export GOPATH=~/Gocode" >> ~/.bash_profilesource ~/.bash_profile
```
上述的代码将会指定你的`GOPATH`环境变量为在你的家（home）目录下的`Gocode`文件夹。然后重新载bash_profile文件以激活配置。

> 不同shell
> 
> 如果你不使用bash，上述的代码可能会失效。比如安装了别的shell例如zsh，你可以google查询zsh的配置方式。如果是你自己写的shell，想必你也指定如何设置啦


#### Windows

Windows8中设置环境变量，只需要在**桌面**左下角右键，选择**系统**->**高级系统设置**->，然后选择**高级**选项卡（tab），然后是**环境变量**按钮。如下图1.1

Windows7, Windows Vista, 右键桌面**计算机**图标或者开始菜单。选择**属性**然后选择**高级系统设置**，然后是**高级**选项卡，最后是**环境变量**按钮。

![windows环境变量菜单](./images/1.1.png)

一旦打开了环境变量设置窗口，选择在**系统变量**中选择**新建**，然后创建一个新的变量命名为`GOPATH`，变量的值为你的go代码工作区的路径，如下图，我设置`C:\Gocode`为`GOPATH`。

![创建新的环境变量](./images/1.2.png)

### 第一份Go代码

本章将会介绍一些基本的go语法，以及使用go写代码的一些常用工具。该介绍只涉及一些基础的知识，而不是全面的go语言教程。随着我们逐步贯穿此书，会逐渐介绍所遇到的概念知识。

任何一门编程的书都会起始于“Hello World”例子，因此让我们跟随巨人的脚步，开启go编程第一步。创建一个文件---`helloworld.go`，然后键入如下代码：

helloworld.go

```
package mainimport "fmt"func main() {    fmt.Println("Hello World")}
```

然后使用命令行打开hellowworld.go所在的目录，运行代码：

```
go run helloworld.go
```

运行成功就会在命令行打印输出`Hello World`。麻雀虽小，五脏俱全，这个简单的程序宝包含了go程序的基本结构。代码开头，我们声明了代码所属的包（package）名。包是我们组织代码的基础结构，`main`包则是特殊的包，它可以直接执行。如果想要写一个包在别的Go程序中使用，必须指定一个唯一的`main`包。后面的章节将会介绍如何写我们自己的包。

开头的下一行，我们导入（import）了程序所使用的包。因为这是一个简单程序，我们只应引用了一个包：`fmt`。`fmt`包来自Go标准库，后者随着go语言安装的时候一起安装。它提供了基本的格式化输出打印操作。`fmt`是标准库的一部分，是一个基础的导入语句。随后，我们将会见识到go如何通过源码url导入第三方包的导入语句；例如：“import github.com/tools/godep”。

最后，我们定义了一个`main`函数，函数中使用了`fmt`包的`Println`函数。main函数是go程序的入口点，当程序启动的时候会执行main函数。`Println`将会打印传入变量的值，你可以传入任何变量。

至此，你可能注意到了go语法的一些字符。首先，括号和花括号和类C的语言很像。不过，你会发现每一句代码结束时并没有分号，每一句结束的下一行为新的语句的开始。最后你会发现代码编译和运行的时间都很快。这是go团队早期的决策之一，让go牺牲一些性能一遍确保提升代码编译速度，这让go在开发程序的时候更有乐趣。

## Go 工具

我们已经见识了第一个go工具（tools）的例子。我们使用go命令行工具运行`.go`文件。`go run`将会编译并运行代码。如果想要创建可执行文件取代每次run文件，可是使用命令`go build`。该命令将会编译当前文件夹下的所有文件，并创建一个以当前文件夹命名的可行性的二进制文件。例如，`chapter1`文件下创建了`helloworld.go`文件，运行`go build`，将会得到一个名为`chapter1`的可行性文件。进一步可以使用`go install`命令，该命令会把编译生成的二进制文件移动到`$GOPATH/bin`文件夹内。如果该文件夹在系统的`PATH`环境变量内，你就可以在任何路径下执行运行这个编译后的go程序。

> PATH 环境变量
> 
> PATH 环境变量是系统寻找可行性文件的路径。当你在命令行输入某个命令的时候，系统会在PATH目录下寻找命令，并执行所找到的第一个命令，如果找不到就会报错。在windows中，你也可以设置PATH包含GOPATH。在MacOS 和Linxu中可以使用早先介方式添加： `export PATH=$PATH:$GOPATH/bin`追加到你的bash profile文件中。

## 基本类型（Types）
Go是一门**强类型**语言。这意味着任何变量止只能存储单一类型的值，当然有时候你需要在不同类型之间进行转换。一旦变量声明后，该变量只能赋值所声明的类型。Go提供了丰富的基础类型，通过这些基础类型，你可以轻松的创建自定义类型来扩展基础类型。

### 字串（String）

**字串**是最普遍的基础类型之一。下面创建一个新的变量，并声明赋值为字串：

```
myString := "I'am a string."
```

注意，我们使用冒号（:）和等号（=）的方式，将一个字串赋值给变量**myString**。`:=`该符号可以声明并初始化一个新的变量。如果你想要修改已经声明初始化**myString**变量的值，重新赋值的时候需要删除冒号。如果仍然保留冒号，等于再次声明一个变量，将导致编译失败：

```
myString := "I’m a string."myString = "I’m really a string, I promise."
```

尝试重新声明初始化变量，编译代码的时候将会收到“`:=`左边没有性的变量”的错误提示。

可以使用`+`符号连接字串。

```
myString := "I’m a string."myOtherString := myString + " I really am."fmt.Println(myOtherString) // 输出 "I’m a string. I really am."
```

> Go注释
> 
> Go支持单行和多行注释，`//`用于单行注释，多行注释的首尾巴使用`/*`和`*/`包裹

### 数字（Number）

Go有很多表示数字的类型。我们归纳为有两大类别：整型（integer）和浮点型(float)。所有不包含小数部分的数字都是**整型**，如`1`， `-7`，和`42`。浮点型则包含小数部分的数字，例如`3.141`或者`-9.2`。

#### 整型（Integer）

每一类数字，都有若干类型。整型有最多的类型：`int`, `int8`, `int16`, `int32`, `int64`, `uint`, `uint8`, `uint16`, `uint32`, 和`uint64`。每一个类型所存储的数字大小是不一样的，主要是基于他们的内存容量是8位（bit）还是16位或32位，64位。例如`int8`可以存储 -128到127之间的数字。而int64可以存储- 9223372036854775808到9223372036854775807之间的数字。任何以`int`开头的整型都是无符号类型，即可以存储正数也可以存储负数，而以`uint`开头的则是无符号类型，只能表示正整数。

事先知道变量的数值的范围可以选择声明合适的变量类型，以减少内存消耗。可是，你会发现通常你都会使用`int64`或者`int`类型。

> 特殊的int
> 
> int是特殊的整型，它的存储范围依赖于计算机的架构。通常你将会使用64位的架构，那么`int`和`int64`是等价的。同理对于`uint`也适用。


#### 浮点型（Float）

浮点型只有两种，`float32`和`float64`。`float64`比`float32`更适用，例如处理很多小数部分的时候。

不同类型之间是不能直接运算操作的。否则将会得到一个编译错误“nvalid operation: a * b (mismatched types int and float64).”即无效的操作，a是int类型，b是float64类型，两者不能相加。想要相加，必须通过强制类型转换：

```
myInt := 2myFloat := 1.5myOtherFloat := float64(myInt) * myFloatfmt.Println(myOtherFloat) // 输出 3
```

> 类型转换
> 
> 别的语言通常使用一种叫“casting”的类型转换手段。需要转换的变量前面用一对圆括号包裹将要转换的的目标类型。这种处理只适用于同一种类别的类型转换，比如都是数字类型。不同类型之间的转换会产生编译错误。后面我们将会介绍更多关于类型转换的例子。

### 布尔（Boolean）

**布尔** 类型相当于预先定义的两个常量：`true`或者`false`。在条件判断中，它们扮演了重要角色，除此之外没有什么可说的。

```
myBool := trueif myBool {    fmt.Println("myBool is true")} else {    fmt.Println("myBool isn’t true")}
```


### 数组（Aarry）和切片（Slice）

**数组**是go中有趣的主题。通常你大部分时间都在处理**切片**，切片只是底层数组的一部分部分或者全部的引用，与大多数编程语言的数组类似。因为在你的日常编程中都是处理切片，我将会跳过一些关于数组的介绍。可是你要是想深入理解切片的数据模型，推荐阅读Go团队的文章[Go Slices: usage and internals](https://blog.golang.org/go-slices-usage-and-internals)。

切片使用`[]T`的格式定义，T表示切片所存储的元素的类型。切片的元素必须是同一类型。下面创建一个切片，然后通过切片再创建新的切片：

```
mySlice := []int{1, 2, 3, 4, 5}mySlice2 := mySlice[0:3]mySlice3 := mySlice[1:4]fmt.Println(mySlice2, mySlice3, mySlice[2])// 输出: [1 2 3] [2 3 4] 3
```

首先，创建了一个包含5个整型元素的切片。花括号里写元素是Go实例化结构的方式，后面很多类似的容器类型都使用这种方式创建类型实例。


创建了第一个切片之后，我们就能通过它创建其他的切片。方括号中的冒号前后的数字是对切片（slice）进行切片（slicing）的起始索引和终止索引。
方括号中只有一个元素则是读取切片的一个元素的引用。使用超过切片长度的索引，程序运行的时候将会遇到索引越界的错误：“panic: runtime error: index out of range”。与多数编程语言类似，索引从0开始而不是1。> 运行时（Runing）错误和编译时（Compile）错误
>
> 编译器很聪明，它对我们的程序很了解，对于有问题的代码，它会拒绝编译。可是如果访问切片非法的索引，这是运行时错误。切片是动态改变大小的，因此go无法在编译的时候推断切片的大小。综上所述，使用切片索引的时候务必小心谨慎，记得检查切片长度。

可以使用内建（built-in）的`len`函数获取切片的长度：

```
mySlice := []int{1, 2, 3, 4, 5}fmt.Println(len(mySlice)) // 输出: 5mySlice := []string{"Hi", "there"}fmt.Println(len(mySlice)) // 输出: 2
```

#### 循环（Loop）

使用`for`语句配合`range`对切片进行迭代。

```
animals := []string{"Cat", "Dog", "Emu", "Warthog"}for i, animal := range animals {    fmt.Println(animal, "is at index", i)}
```

输出：

```
Cat is at index 0Dog is at index 1Emu is at index 2Warthog is at index 3
```

如果不想使用索引`i`的值，例如不对`i`赋值或者赋值了忽略不使用。我们会得到一个错误“i declared and not used”，`i`（变量声明了但是并没有使用）。若确定不在循环内使用变量索引，可以把索引赋值给一个下划线`_`符号，表示值被忽略。空下划线符号用于声明了但不使用的变量：

```
animals := []string{"Cat", "Dog", "Emu", "Warthog"}for _, animal := range animals {    fmt.Println(animal)}
```

### 图（Map）

Go提供了**图**结构用于存储键值对（key/value）数据。图和其他语言的哈稀表结构类似，或者是`Javascript`中的对象（object）。图的定义需要指定key和value的类型，像这样的结构`map[string]int`。例如，想要存储星球大战（Star Wars）电影发布的年数，可以创建如下图结构：

```
starWarsYears := map[string]int{
	"A New Hope":              1977,
	"The Empire Strikes Back": 1980,
	"Return of the Jedi":      1983,
	"Attack of the Clones":    2002,
	"Revenge of the Sith":     2005,
}
```

往图增加新的元素只需这样：

```
starWarsYears["The Force Awakens"] = 2015
```

注意，赋值并没有使用`:=`符号。

与切片类似，使用`len`函数获取图的大小

```
fmt.Println(len(starWarsMovies)) // 输出: 6
```

#### 图的循环

图的循环和切片的迭代类似。使用`for`语句配合`range`，不同在于，图的键取代了切片迭代的索引作为range返回的第一个值：

```
for title, year := range starWarsYears {	  fmt.Println(title, "was released in", year)}
```

运行上述代码，输出如下：

```
Revenge of the Sith was released in 2005The Force Awakens was released in 2015A New Hope was released in 1977
The Empire Strikes Back was released in 1980Return of the Jedi was released in 1983Attack of the Clones was released in 2002
```
再一次运行代码，会发现输出的顺序与之前的不一样了。与数组和切片不一样，图的元素是没有先后顺序的，理解这个很重要。实际上，开发者必须明确了解，图使用随机顺序遍历图的元素。

#### 图的处理

使用图的方括号传入key的方式读取对应的value：

```
colours := map[string]string{    "red":    "#ff0000",    "green":  "#00ff00",    "blue":   "#0000ff",    "fuchsia": "#ff00ff",}redHexCode := colours["red"]
```
如果key `red`不存在，读取将会返回会是“空值”（empty value），这里变量`redHexCode`键对应的值将是空字串。

使用内建函数`delete`删除图的键值对。
```
function: delete(colours, "fuchsia")
```

`delete`函数不会返回任何信息，即使传入的key不存在而删除失败也不会返回任何信息。想要知道图的key是否存在，读取的时候可以使用特殊的双返回值；第二个值是一个布尔值，表示key存在与否。

```
code, exists := colours["burgundy"]if exists {    fmt.Println("Burgundy's hex code is", code)
} else {    fmt.Println("I don't know burgundy")}
```

## 函数（Function）

我们已经在本章的开篇的HelloWorld练习中见识了函数。现在更深一点点了解函数吧。

函数使用关键字（keyword）`func`定义，它可以传递多个参数和返回多个值。每一个参数和返回的值都必须指定类型；如果参数列表都是同一种类型，只需要在最后的参数指定类型即可。下面有几个例子：

```
func noParamsNoReturn() {    fmt.Println("I’m not really doing much!")}func twoParamsOneReturn(myInt int, myString string) string {    return fmt.Sprintf("myInt: %d, myString: %s", myInt, myString)}func oneParamTwoReturns(myInt int) (string, int) {    return fmt.Sprintf("Int: %d", myInt), myInt + 1}func twoSameTypedParams(myString1, myString2 string) {    fmt.Println("String 1", myString1)    fmt.Println("String 2", myString2)}
```

上述的例子中，第一个函数没有参数和返回值；这是最简单的一类函数。`twoParamsOneReturn`函数有两个不同类型的参数，并返回一个`string`类型的值。`oneParamTwoReturns`函数有一个`int`类型的参数，同时返回了一个`string`类型和一个`int`类型的返回值。最后，`twoSameTypedParams`函数展示了两个相同类型的参数，只需要在最后一个参数指定类型即可。

很多函数都会返回两个值，第一个是函数实际需要返回的值，第二个值则是表示函数执行式是否有错误发生。这种方式在GO的实践中非常普遍，稍后我们再展示如何处理返回的错误。尽管你可以两个以上的值，可是这样的做法不常见。


### 指针（Pointer）


当你把一个变量以参数传给函数的时候，实际上传的是变量的副本，而不是变量本身。即使在函数内改变了这个变量的值，调用函数的时候，函数外并变量的值并没有被改变。

指针（Pointers）可以让你传入参数变量对象的引用，而不是传对象本身。这意味着你可以改变函数内对象的值，函数代码运行之后，变量将会更新其值。如果你之前的编程语言也支持指针操作，你一定很熟悉被称之为“传值还是传引用”（passing by reference）的概念。


指针的最好解释来自我们日常生活场景：你有一个香蕉，一个梨，一个仓库和锁，以及一台克隆机。你创建一个`myFruit`仓库变量，并存放一个香蕉。然后把仓库变量传给克隆机。它随后从克隆机出来。假设又有一个仓库变量`myClonedFruit`则存放了一个梨。现在`myFruit`里有一个香蕉而`myClonedFruit`则有一个梨。修改`myClonedFruit`中任何东西都不会对`myFruit`造成影响。也许你已经猜到，这就是等同于把`myFruit`变量传入到函数（克隆机）所发生一样。函数创建了一个新的变量，这个变量是参数的拷贝，改变这个新变量对原始的变量毫无影响。

现在，让我们再看看给仓库加上锁会发生什么。我们会从头开始，所以忘了前面的两个变量。我们创建一个`myFruit`仓库变量，并存放一个香蕉，然后把仓库变量给锁上。并把锁传给克隆机，克隆机也得到一个为`myClonedFruit`仓库变量。此时克隆机并没有复制一个新的`myFruit`仓库变量，而是把传入的锁的复制了一遍并也锁上`myClonedFruit`。然后往通过锁往`myClonedFruit`变量里放入一个梨。现在我们还是有两个变量`myFruit`和`myClonedFruit`，可是它们里面都只存放了一个梨，因为他们使用的是同一把锁。（译者注：作者的意思是克隆机修改的操作的时候，会通过锁寻找仓库，然后修改仓库，复制的是锁，锁打开的其实是同一个仓库，`myFruit`和`myClonedFruit`其实是一个变量，读取和修改他们的值都是通过锁进进行操作）

第二个例子中，传递水果变量的指针取代了传递水果变量本身。这个指针指向水果变量所存储内存的地址，因此我们可以通过地址改成这个变量的值，函数和函数外的代码都读取同一个变量的值。

Go代码中将如何实现呢？看下面的例子：

```
func giveMePear(fruit string) {    fruit = "pear"}func main() {    fruit := "banana"    giveMePear(fruit)    fmt.Println(fruit) // 输出: banana}

```

这个例子把`fruit`变量传递给了`giveMePear`函数，后者得到的其实是`fruit`变量的拷贝。

```
func giveMePear(fruit *string) {    *fruit = "pear"}func main() {    fruit := "banana"    giveMePear(&fruit)    fmt.Println(fruit) // Outputs: pear}
```

第二个例子中，传给`giveMePear`函数不再是一个`string`类型参数，而是一个`string`类型的指针---使用星号`*string`声明类型。函数里我们使用了一个新的字串赋值给指针引用参数，使用`*`读取指针变量所引用的值。当调用函数的时候，传递的并不是`fruit`变量的拷贝，而是该变量的地址的拷贝。使用`&`符号在变量之前的形式传地址。其含义是告诉`Go`，对变量本身并不感兴趣，只对指向变量内存地址的指针干兴趣。

如果你尚未完全掌握指针的概念，不要担忧，我们很快就会实践中应用，我希望到时你能通过持续学习本书过程中理解。

> nil 指针
> 
> 还有一点需要注意，使用指针的时候并不能保证一定要传一个值给函数。也可以传`nil`，它表示没有值（注意，这和`false`不一样，后者只使用与布尔类型）。我们的例子中很明细没有传入的指针你是nil。但是，你使用的变量很可能那个是别的代码所传入的值，因此你必须检查是否实际传递了值。读取或改变nil指针将会报错：“panic: runtime error: invalid memory address or nil pointer dereference”（运行时错误，非法的内存地址或者nil指针）。避免这个错误需要检查传递的变量是否等于nil。

## 结构（Struct）

Go允许自定义类型，所有自定义类型都是结构。结构是包含命名字段的类型。继续前面的电影例子，我们可以创建一个Movie类型，它里面有一些数据：


```
type Movie struct {    Actors      []string    Rating      float32    ReleaseYear int    Title       string}
```

如您所见，我们还创建了多种不同的类型数据字段，每一个字段都有着自己的类型。你还会注意到每一个字段名都是以大写字母开头。这个规则很重要，这预示着这些值可以被包外的代码所访问。这些字段是可以导出的，我们会在接下来的章节介绍可导出与不可导出的实际关系。你可以粗略的理解，是否可以导出的字段或者方法类似访问权限的`public`（公有）还是`private`（私有）。

与切片和图实例的方式类似，创建`Movie`类型的实例只需要在花括号中写入初始值即可：

```
episodeIV := Movie{    Title:       "Star Wars: A New Hope",    Rating:      5.0,    ReleaseYear: 1977,}
```

我们有了一个`Movie`实例，赋值给了`episodeIV`变量。我们值提供了`Movie`四个字段中的三个字段初始值，因此第四个字段将会根据其类型自动初始化为其空值，即`nil`。

对于已经实例化的变量， 可以通过`.`点操作符访问它的成员字段，即读取字段的值或给字段赋值：
```
episodeIV.Actors = []string{    "Mark Hamill",    "Harrison Ford",    "Carrie Fisher",}fmt.Println(episodeIV.Title, "has a rating of", episodeIV.Rating)
```


### 方法（Method）

你可以给任何自定义的类型添加方法。这与定义函数一样简单，这个方法有一个接受者（reciver）。所谓接受者类型很像是函数中定义只有一个参数的形式，只不过这个声明在`func`关键字之后，函数名之前。例如给Movie类型定义一个方法DisplayTitile，该方法用于打印一些格式化电影的名字和发行年限，可以写成如下的形式：

```
func (movie Movie) DisplayTitle() string {    return fmt.Sprintf("%s (%d)", movie.Title, movie.ReleaseYear)}

func main() {    episodeV := Movie{        Title:       "Star Wars: The Empire Strikes Back",        ReleaseYear: 1980,    }    fmt.Println(episodeV.DisplayTitle())    // 输出: “Star Wars: The Empire Strikes Back (1980)”}
```
如您所见，在函数名`DisplayTitle`之前，声明了一个接受者`(movie Movie)`。这里声明了一个`Movie`类型的变量`movie`，可以像函数的其他参数一样在函数体内使用。刚接触方法可能让你感到头疼，其实这并不是新概念，这很像其他面对对象语言里类的“this”或者“self”。

> Go中使用面对对象
> 
> 接受者函数是Go里实现面对对象的基础。定义了接受函数方法的类型，如同面对对象里的**对象**。我必须指出，Go并没有提供很多传统面对对象编程的结构，例如**继承**，go就是这么设计的。Go提供了很多**方法**用于实现复杂的数据类型，诸如以后会学习的**内嵌类型**（embedded types）和**接口**（interface）


接受者类型也可以是一个指针类型。如果接受者不是指针，方法内任对结构实例的修改都只存在方法函数中，方法外的代码将不受影响。一个直观的列子就是定义一个计算（counter）类型，提供`Increment`方法给类型的`count`字段加一。

```
type Counter struct {    Count int}
func (c Counter) Increment() {    c.Count++}
func (c *Counter) IncrementWithPointer() {    c.Count++}

func main() {    counter := &Counter{}    fmt.Println(counter.Count) // 输出: 0    counter.Increment()    fmt.Println(counter.Count) // 输出: 0    counter.IncrementWithPointer()    fmt.Println(counter.Count) // 输出: 1}
```

如您所见，调用`Increment`方法的时候，接受者为Counter实例的拷贝，在`Increment`方法作用域外，字段`Count`并没有增加。一旦方法接受者是一个指针类型，修改同样的`IncrementWithPointer`方法内修改的`Counter`和方法外的是同一个实例对象。

这很有趣，创建`Counter`实例的时候使用了取址符号`&`，因此我们可以同时调用不包含指针接受者的`Increment`，和包含指针接受者的`IncrementWithPointer`方法。如果创建实例使用表达式`counter := Counter{}`，那么将无法调用`IncrementWithPointer`方法。（译者注：Go1.6.3版本counter := Counter{}也可以调用这两个方法）

## 代码可导性

当你写自己的包，结构的时候，你需要考虑什么样的方法，函数，常量将提供给包以外的作用域的代码访问。所谓**可导出**（exported）的值指的是在包以外的作用域也可以访问，顾名思义**不可导**（enexported）的值则相反。当你不确定一个变量是否需要导出给别的代码访问的时候，一个显而易见的规则就是都设置成不可导出，直到意识到外面的包需要使用的时候再重新修改名字。

```
// myUnexportedFunc 是小写字母开头，其作用域只在包内，无法导出func myUnexportedFunc() {}// MyExportedFunc 是大写字母开头的，对其他包也是可见的，即可以导出func MyExportedFunc() {}type MyExportedType struct{
    ExportedField   string    unexportedField string}
```

## 总结

本章介绍了Go语法和类型的基础知识。下一章，我们将会学习创建自定义类型，如何使用接口连接不同类型的实现，以及Go如何处理第三方库。








