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

### binary representation

```swift
Int.bitWidth // 64
0b11010.bitWidth // 64
0b11010.nonzeroBitCount // 3
0b11010.leadingZeroBitCount // 59
0b11010.trailingZeroBitCount // 1
```

## Strings and Text

## Collections

## Time
