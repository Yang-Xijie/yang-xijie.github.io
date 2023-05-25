# Swift 教学课后作业

> 2021.10.17 添加作业内容
> 
> 2021.10.25 更新作业答案
>
> 作业：[杨希杰](https://github.com/Yang-Xijie)

## Introduction

* 基础部分为基本要求，进阶部分可自选；题目前有`Optional`也是选做。
* 复制下面对应部分的作业，在括号或空白处中**填空**。

## 基础

### 查文档

〇 Swift官网的网址是（）。我们一般会在官网上查找Swift的文档，即Language Guide，网址为（）。

〇 在Xcode中打开开发者文档的方法是：在菜单栏（）中点击（），或使用快捷键（）。

### 强类型

观察下面的代码：（提示：观察不出来可以实际运行）

```swift
let a = 1
a = 5
var b = 4
b = 4.5
```

〇 代码第二行报错的原因是（）。

〇 代码第四行报错的原因是（）。

### 可选类型

〇 如果变量`a`是一个可选类型，我们可以通过方式（）实现：如果其不为空，则取出真实值赋给`b`；若其为空，则令`b`为`0`：

A. `let b = a!`

B. `let b = (a != nil) ? a : 0`

C. `if let b = a { ... } else { let b = 0  ... }`

D. `if a != nil { b = a!  ... } else { b = 0  ... }`

### 函数

〇 一个函数可以通过（）返回多个值。

〇 编写程序，计算10的阶乘并输出结果。要求：使用`...`运算符。【循环 区间生成运算符】
（

）

〇 回顾函数闭包的相关知识，补全下列代码：

```swift
let fruits: [String] = ["apple", "orange", "pear", "pineapple"]
// 希望打印出 ["pineapple", "orange", "apple", "pear"]
// 即Array中的所有字符串按照长度从大到小排序

// TODO
```

提示：

阅读函数`sorted(by:)`的[文档](https://developer.apple.com/documentation/swift/sequence/2907222-sorted)（`func sorted(by areInIncreasingOrder: (Self.Element, Self.Element) -> Bool) -> [Self.Element]`）

如果你想直接在大括号中写函数的话，`$0`和`$1`可以分别指代第1个和第2个参数。

### 统计各个专业的人数

```swift
import Foundation

enum Major {
    case A
    case B
    case C
    case D
}

struct Student {
    var name: String
    var major: Major
}

let studentList: [Student] = [
    Student(name: "Alice", major: .A),
    Student(name: "Bob", major: .B),
    Student(name: "Carl", major: .C),
    Student(name: "David", major: .D),
    Student(name: "Eric", major: .A),
    Student(name: "Fred", major: .D),
    Student(name: "Gavin", major: .C),
    Student(name: "Henry", major: .D),
    Student(name: "Ivy", major: .B),
    Student(name: "Janet", major: .D),
    Student(name: "Kathy", major: .A)
]

// 题目：
// 统计studentList中各个专业的同学名字和总数目，并按照你倾向的方式打印。

// TODO
```

## 进阶

### Error Handling

执行如下程序，结果为（

）（共两行），简要解释输出结果：（）。

```swift
import Foundation

struct Printer {
    var paper: Int // 0 - 400
    var ink: Float // 0 - 100 percentage
    let inkPerPage: Float = 0.1

    enum error: Error {
        case outOfPaper
        case noInk
    }
}

struct File {
    var name: String
    var page: Int
}

func printFile(_ file: File, with printer: inout Printer) throws {
    if printer.paper <= file.page {
        throw Printer.error.outOfPaper
    } else if printer.ink <= Float(file.page) * printer.inkPerPage {
        throw Printer.error.noInk
    } else {
        printer.paper -= file.page
        printer.ink -= Float(file.page) * printer.inkPerPage
        print("File \"\(file.name)\" was successfully printed! (paper: \(printer.paper), ink: \(String(format: "%2.1f", printer.ink))%)")
    }
}

var myHomework = File(name: "my homework", page: 4)
var myReport = File(name: "my report", page: 5)
var myPrinter = Printer(paper: 7, ink: 80)
do {
    try printFile(myHomework, with: &myPrinter)
    try printFile(myReport, with: &myPrinter)
} catch {
    print(error)
}
```

### Log()

新建`Project - macOS - Command Line Tool`，复制运行如下代码：

```swift
import Foundation // 1

struct Log: CustomStringConvertible { // 3
    public var time: String // 4
    public var log: String // 5

    init(filePath: String = #file, line: Int = #line, column: Int = #column, funcName: String = #function) { // 7
        let fileName = (filePath as NSString).lastPathComponent // 8

        let formatter = DateFormatter() // 10
        formatter.dateStyle = .none // 11
        formatter.timeStyle = .medium // 12
        time = formatter.string(from: Date()) // 13

        log = "\(fileName)(\(line),\(column)) \(funcName)" // 15
    }

    public var description: String { // 18
        return "[\(time) \(log)]\n\t" // 19
    }

    public var string: String { // 22
        description // 23
    } // 24

    public var error: String { // 26
        "[ERROR] " + description // 27
    }
}

func MyPrint() { // 31
    print(Log().string + "Hello, world!") // 32
    print(Log().error + "Bye, world.") // 33
}

MyPrint() // 36

// Literal        Type     Value
//
// #file          String   The name of the file in which it appears.
// #line          Int      The line number on which it appears.
// #column        Int      The column number in which it begins.
// #function      String   The name of the declaration in which it appears.
```

〇 该程序的运行结果是（

）。

〇 第3行新建了一个结构体名为Log，后面冒号跟着的`CustomStringConvertible`是（），在结构体内部的变量（）完成了`CustomStringConvertible`。

〇 （Optional）可以去掉第4行的`public`关键字吗？（）

〇 第7行中，`filePath: String = #file`中`filePath`是参数名称，冒号后面的`String`是这个参数的（），`=`后面跟的是这个参数的（）。

〇 （Optional）第8行中，`(filePath as NSString)`是在做（）。

〇 第12行中出现了`.medium`，它们是（）的一种。

〇（Optional）第12行如果要补全`.`前面的内容可以添加（）。提示：查看`.medium`的文档。

〇 第13行中的`formatter.string(from: )`，这里string是一个（），看到`from`这一个介词可以推测`from`是参数的（）。

〇 第19行的`\n`和`\t`是（）字符。

〇 第22行定义了变量string，我们将其称作（计算属性）。将22 23 24这三行代码补充完整：（

）。

〇 第32行的`Log()`（）了一个结构体实例。

〇 第32行的`+`表示（）。

〇 第36行调用了函数`MyPrint`，该函数有（）个参数，（）个返回值。

〇 （Optional）尝试如下步骤在`Xcode`中添加`code snippet`：

To create a `code snippet`:

1. Select: print(Log().string + "<\hashinfo\hash>")
2. Go to `Xcode -> Editor -> Create Code Snippet`.
3. Change `\hash` to `#`.
4. Set title as `Log()` and `completion` as `print`.

Try typing `print` and select the code snippet.

## 其他

〇 （Optional）如果我们想导入并使用一个开源的第三方`Swift Package`，需要点击`Xcode`菜单栏（）（写出层级关系），然后添加该`Swift Package`的地址。之后在需要用到该包的代码文件最开始写上`import`语句就可以了。

〇 `Swift`有一个非常好用的格式化工具[GitHub | SwiftFormat](https://github.com/nicklockwood/SwiftFormat)，阅读其README说明，在自己的Xcode中添加该格式化工具并尝试使用。你在你的`Mac`上安装了吗？（）（安装了/还没/下次一定）。

〇 （Optional）`Swift`目前的最新版本是`5.5`，这一个版本引入的一个重要更新是Concurrency WWDC链接[WWDC21 | Meet async/await in Swift](https://developer.apple.com/wwdc21/10132)，感兴趣的同学可以自行查看。

〇 （Optional）如果你还没有学习过Git，可以花时间掌握一下这个合作开发的必备工具。社团往期培训课程传送门 [Git基础与进阶](https://www.bilibili.com/video/BV1eh411v7gt)

---

## 答案

## 基础

### 查文档

〇 Swift官网的网址是（<https://swift.org>）。我们一般会在官网上查找Swift的文档，即Language Guide，网址为（<https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html>）。

〇 在Xcode中打开开发者文档的方法是：在菜单栏（`Window`）中点击（`Developer Documentation`），或使用快捷键（`shift cmd 0`）。

### 强类型

观察下面的代码：（提示：观察不出来可以实际运行）

```swift
let a = 1
a = 5
var b = 4
b = 4.5
```

〇 代码第二行报错的原因是（`a是一个常量无法更改`）。

〇 代码第四行报错的原因是（`由类型推断机制，b的类型为Int，无法将小数4.5赋值给b`）。

### 可选类型

〇 如果变量`a`是一个可选类型，我们可以通过方式（`BCD`）实现：如果其不为空，则取出真实值赋给`b`；若其为空，则令`b`为`0`：

A. `let b = a!`

B. `let b = (a != nil) ? a : 0`

C. `if let b = a { ... } else { let b = 0  ... }`

D. `if a != nil { b = a!  ... } else { b = 0  ... }`

### 函数

〇 一个函数可以通过（`元组`）返回多个值。

〇 编写程序，计算10的阶乘并输出结果。要求：使用`...`运算符。提示：循环 区间生成运算符
（
```swift
var result: Int = 1
for i in 2 ... 10 {
    result *= i
}

print(result)
```
）

〇 回顾函数闭包的相关知识，补全下列代码：

```swift
let fruits: [String] = ["apple", "orange", "pear", "pineapple"]
// 希望打印出 ["pineapple", "orange", "apple", "pear"]
// 即Array中的所有字符串按照长度从大到小排序

// TODO
```

提示：

阅读函数`sorted(by:)`的[文档](https://developer.apple.com/documentation/swift/sequence/2907222-sorted)（`func sorted(by areInIncreasingOrder: (Self.Element, Self.Element) -> Bool) -> [Self.Element]`）

如果你想直接在大括号中写函数的话，`$0`和`$1`可以分别指代第1个和第2个参数。

答案：

```swift
print(fruits.sorted(by: { $0.count > $1.count }))
```
或
```swift
func longer(a: String, b: String) -> Bool {
    return a.count > b.count
}

print(fruits.sorted(by: longer))
```

### 统计各个专业的人数

```swift
import Foundation

enum Major {
    case A
    case B
    case C
    case D
}

struct Student {
    var name: String
    var major: Major
}

let studentList: [Student] = [
    Student(name: "Alice", major: .A),
    Student(name: "Bob", major: .B),
    Student(name: "Carl", major: .C),
    Student(name: "David", major: .D),
    Student(name: "Eric", major: .A),
    Student(name: "Fred", major: .D),
    Student(name: "Gavin", major: .C),
    Student(name: "Henry", major: .D),
    Student(name: "Ivy", major: .B),
    Student(name: "Janet", major: .D),
    Student(name: "Kathy", major: .A)
]

// 题目：
// 统计studentList中各个专业的同学名字和总数目，并按照你倾向的方式打印。

// TODO
```

一种解答：

```swift
var studentDict: [Major: [Student]] = [Major.A: [], Major.B: [], Major.C: [], Major.D: []]

for student in studentList {
    switch student.major {
    case .A:
        studentDict[.A]!.append(student)
    case .B:
        studentDict[.B]!.append(student)
    case .C:
        studentDict[.C]!.append(student)
    case .D:
        studentDict[.D]!.append(student)
    }
}

for major in [Major.A, Major.B, Major.C, Major.D] {
    let students = studentDict[major]!
    let studentNames = students.map { $0.name }
    print("\(major)(\(students.count)): \(studentNames.joined(separator: ", "))")
}
```

## 进阶

### Error Handling

执行如下程序，结果为（
```
File "my homework" was successfully printed! (paper: 3, ink: 79.6%)
outOfPaper
```
）（共两行），简要解释输出结果：（`作业打印之后打印机的纸张不足以打印报告，因此抛出错误 outOfPaper`）。

```swift
import Foundation

struct Printer {
    var paper: Int // 0 - 400
    var ink: Float // 0 - 100 percentage
    let inkPerPage: Float = 0.1

    enum error: Error {
        case outOfPaper
        case noInk
    }
}

struct File {
    var name: String
    var page: Int
}

func printFile(_ file: File, with printer: inout Printer) throws {
    if printer.paper <= file.page {
        throw Printer.error.outOfPaper
    } else if printer.ink <= Float(file.page) * printer.inkPerPage {
        throw Printer.error.noInk
    } else {
        printer.paper -= file.page
        printer.ink -= Float(file.page) * printer.inkPerPage
        print("File \"\(file.name)\" was successfully printed! (paper: \(printer.paper), ink: \(String(format: "%2.1f", printer.ink))%)")
    }
}

var myHomework = File(name: "my homework", page: 4)
var myReport = File(name: "my report", page: 5)
var myPrinter = Printer(paper: 7, ink: 80)
do {
    try printFile(myHomework, with: &myPrinter)
    try printFile(myReport, with: &myPrinter)
} catch {
    print(error)
}
```

### Log()

新建`Project - macOS - Command Line Tool`，复制运行如下代码：

```swift
import Foundation // 1

struct Log: CustomStringConvertible { // 3
    public var time: String // 4
    public var log: String // 5

    init(filePath: String = #file, line: Int = #line, column: Int = #column, funcName: String = #function) { // 7
        let fileName = (filePath as NSString).lastPathComponent // 8

        let formatter = DateFormatter() // 10
        formatter.dateStyle = .none // 11
        formatter.timeStyle = .medium // 12
        time = formatter.string(from: Date()) // 13

        log = "\(fileName)(\(line),\(column)) \(funcName)" // 15
    }

    public var description: String { // 18
        return "[\(time) \(log)]\n\t" // 19
    }

    public var string: String { // 22
        description // 23
    } // 24

    public var error: String { // 26
        "[ERROR] " + description // 27
    }
}

func MyPrint() { // 31
    print(Log().string + "Hello, world!") // 32
    print(Log().error + "Bye, world.") // 33
}

MyPrint() // 36

// Literal        Type     Value
//
// #file          String   The name of the file in which it appears.
// #line          Int      The line number on which it appears.
// #column        Int      The column number in which it begins.
// #function      String   The name of the declaration in which it appears.
```

〇 该程序的运行结果是（
```
[23:51:18 main.swift(32,14) MyPrint()]
	Hello, world!
[ERROR] [23:51:18 main.swift(33,14) MyPrint()]
	Bye, world.
Program ended with exit code: 0
```
）。

〇 第3行新建了一个结构体名为Log，后面冒号跟着的`CustomStringConvertible`是（`协议`），在结构体内部的变量（`description`）完成了`CustomStringConvertible`。

〇 （Optional）可以去掉第4行的`public`关键字吗？（可以。这里加上`public`是为了使得变量属性更加明确。）

〇 第7行中，`filePath: String = #file`中`filePath`是参数名称，冒号后面的`String`是这个参数的（`类型`），`=`后面跟的是这个参数的（`默认值`）。

〇 （Optional）第8行中，`(filePath as NSString)`是在做（`类型转换`）。

〇 第12行中出现了`.medium`，它们是（`枚举值`）的一种。

〇（Optional）第12行如果要补全`.`前面的内容可以添加（`DateFormatter.Style`）。提示：查看`.medium`的文档。

〇 第13行中的`formatter.string(from: )`，这里`string`是一个（`函数`），看到`from`这一个介词可以推测`from`是参数的（`外部名称`）。

〇 第19行的`\n`和`\t`是（`转义`）字符。

〇 第22行定义了变量string，我们将其称作（计算属性）。将22 23 24这三行代码补充完整：（
```swift
public var string: String {
    get {
        return description
    }
}
```
）。

〇 第32行的`Log()`（`新建`）了一个结构体实例。

〇 第32行的`+`表示（`字符串拼接`）。

〇 第36行调用了函数`MyPrint`，该函数有（`0`）个参数，（`0`）个返回值。

〇 （Optional）尝试如下步骤在`Xcode`中添加`code snippet`：

To create a `code snippet`:

1. Select: print(Log().string + "<\hashinfo\hash>")
2. Go to `Xcode -> Editor -> Create Code Snippet`.
3. Change `\hash` to `#`.
4. Set title as `Log()` and `completion` as `print`.

Try typing `print` and select the code snippet.

## 其他

〇 （Optional）如果我们想导入并使用一个开源的第三方`Swift Package`，需要点击`Xcode`菜单栏（`File -> Swift Packages -> Add Package Dependency...`）（写出层级关系），然后添加该`Swift Package`的地址。之后在需要用到该包的代码文件最开始写上`import`语句就可以了。

〇 `Swift`有一个非常好用的格式化工具[GitHub | SwiftFormat](https://github.com/nicklockwood/SwiftFormat)，阅读其README说明，在自己的Xcode中添加该格式化工具并尝试使用。你在你的`Mac`上安装了吗？（）（安装了/还没/下次一定）。

〇 （Optional）`Swift`目前的最新版本是`5.5`，这一个版本引入的一个重要更新是Concurrency WWDC链接[WWDC21 | Meet async/await in Swift](https://developer.apple.com/wwdc21/10132)，感兴趣的同学可以自行查看。

〇 （Optional）如果你还没有学习过Git，可以花时间掌握一下这个合作开发的必备工具。社团往期培训课程传送门 [Git基础与进阶](https://www.bilibili.com/video/BV1eh411v7gt)