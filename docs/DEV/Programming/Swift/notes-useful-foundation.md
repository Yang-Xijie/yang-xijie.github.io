---
title: Swift笔记 ｜ 标准库常用函数
---

# Swift笔记 ｜ 标准库常用函数

> [Swift Standard Library](https://developer.apple.com/documentation/swift/swift-standard-library) Values and Collections

## Numbers and Basic Values

### Bool

```swift
var isPresenting = Bool.random() // https://developer.apple.com/documentation/swift/bool/random()
isPresenting.toogle() // https://developer.apple.com/documentation/swift/bool/toggle()
```

### Int

#### init

用Double初始化时向0靠近

```swift
// https://developer.apple.com/documentation/swift/int/init(_:)-8vbwo
let x = Int(21.5) // x == 21
let y = Int(-21.5) // y == -21
```

使用x进制表示的字符串初始化Int

```swift
// https://developer.apple.com/documentation/swift/int/init(_:radix:)
let a = Int("100", radix: 2)! // a == 4
let b = Int("FF", radix: 16)! // b == 255
```

生成范围内随机整数

```swift
let a = Int.random(in: 1..<100)
```

常量

```swift
Int.zero // 0
Int.max // 9223372036854775807
Int.min // -9223372036854775808
```

#### calculation

整除

```swift
// https://developer.apple.com/documentation/swift/int/quotientandremainder(dividingby:)
let x = 1_000_000
let (q, r) = x.quotientAndRemainder(dividingBy: 933) // q == 1071, r == 757
```

```swift
// https://developer.apple.com/documentation/swift/int/ismultiple(of:)
15.isMultiple(of: 3) // true
15.isMultiple(of: 4) // false
```

绝对值

```swift
abs(2) // 2
abs(-2) // 2
```

#### binary representation

```swift
Int.bitWidth // 64
0b11010.bitWidth // 64
0b11010.nonzeroBitCount // 3
0b11010.leadingZeroBitCount // 59
0b11010.trailingZeroBitCount // 1
```

### Double

#### init

random

```swift
Double.random(in: 10.0 ..< 20.0)
```

constants

```swift
Double.pi
Double.infinity
Double.nan
```

#### calculation

```swift
4.0.squareRoot() // 2
```

```swift
// https://developer.apple.com/documentation/swift/double/round(_:)
1.5.round(.down)
1.5.round(.up)
1.5.round(.towardZero)
1.5.round(.awayFromZero)
1.5.round(.toNearestOrAwayFromZero)
```

```swift
for radians in stride(from: 0.0, to: .pi * 2, by: .pi / 2) {
    let degrees = Int(radians * 180 / .pi)
    print("Degrees: \(degrees), radians: \(radians)")
}
// Degrees: 0, radians: 0.0
// Degrees: 90, radians: 1.5707963267949
// Degrees: 180, radians: 3.14159265358979
// Degrees: 270, radians: 4.71238898038469
```

### Range

```swift
let underFive = 0.0 ..< 5.0 
underFive.contains(3.14) // true
underFive.lowerBound // 0.0
underFive.upperBound // 5.0
let empty = 0.0 ..< 0.0
empty.isEmpty // true
```

```swift
// 将当前的范围限制在新给定的范围中
func clamped(to limits: Range<Bound>) -> Range<Bound>
// 两个Range范围是否重叠
func overlaps(_ other: Range<Bound>) -> Bool
```

### Global Numeric Functions

```
min(...)
max(...)
abs(...)
```

## Strings and Text

### init

```swift
init(_ c: Character)
init(_ substring: Substring)
init(repeating repeatedValue: String, count: Int)
init(repeating repeatedValue: Character, count: Int)
```

```swift
init<Subject>(describing instance: Subject)
```

```swift
init(decoding path: FilePath)
init(contentsOf url: URL) throws
init(contentsOfFile path: String) throws
```

```swift
String(5, radix: 2) // "101"
String(255, radix: 16) // "ff"
String(255, radix: 16, uppercase: true) // "FF"
```

### properties

```swift
let str = "Hello"
str.count // 5
let empty = ""
empty.isEmpty // true
```

```swift
func lowercased() -> String
func uppercased() -> String
```

```swift
func hasPrefix(_ prefix: String) -> Bool
func hasSuffix(_ suffix: String) -> Bool
func contains<T>(_ other: T) -> Bool where T : StringProtocol // Equivalent to self.range(of: other) != nil
```

```swift
func prefix(_ maxLength: Int) -> Self.SubSequence
func prefix(through position: Self.Index) -> Self.SubSequence
func prefix(upTo end: Self.Index) -> Self.SubSequence
func suffix(_ maxLength: Int) -> Self.SubSequence
func suffix(from start: Self.Index) -> Self.SubSequence
```

### index

```swift
let str = "Hello, world!"
str.startIndex
str.endIndex
```

Character

```swift
let name = "Marie Curie"
let firstSpace = name.firstIndex(of: " ") ?? name.endIndex
let firstName = name[..<firstSpace] // "Marie"
```

String

```swift
let range = "Hello".range(of: "ll")! // 返回第一个查找到的词
print("Hello"[range]) // ll 
```

### modify

```swift
var a = "Hello"
a.append(contentsOf: ", world!")
print(a)
var b = "Hello"
b.insert(contentsOf: ", world!", at: b.endIndex)
print(b)
```

#### replace

```swift
var str = "Hello, world!"
let helloRange = str.range(of: "Hello")!
str.replaceSubrange(helloRange, with: "Welcome")
print(str) // Welcome, world!
```

```swift
var str = "Hello, world!"
let worldRange = str.range(of: ", world")!
str.removeSubrange(worldRange)
print(str) // Hello!
```

```swift
let str = "Hello, world!"
print(str.replacingOccurrences(of: "Hello", with: "Welcome")) // Welcome, world!
```

### other operations

```swift
func split(
    separator: Self.Element,
    maxSplits: Int = Int.max,
    omittingEmptySubsequences: Bool = true
) -> [Self.SubSequence]
```

## Collections



## Time

TODO
