# Swift 笔记 ｜ 标准库常用函数

> [Swift Standard Library](https://developer.apple.com/documentation/swift/swift-standard-library) Values and Collections

- Numbers and Basic Values
- Strings and Text
- Collections
- Time

## Bool

```swift
var isPresenting = Bool.random()
isPresenting.toogle()
```

## Int

### init

#### Double

```swift
let x = Int(21.5) // x == 21
let y = Int(-21.5) // y == -21
```

#### radix

```swift
let a = Int("100", radix: 2)! // a == 4
let b = Int("FF", radix: 16)! // b == 255
```

#### random
```swift
let a = Int.random(in: 1..<100)
```

#### constants

```swift
Int.zero // 0
Int.max // 9223372036854775807
Int.min // -9223372036854775808
```

### calculation

#### quotient

```swift
let x = 1_000_000
let (q, r) = x.quotientAndRemainder(dividingBy: 933) // q == 1071, r == 757
```

```swift
15.isMultiple(of: 3) // true
15.isMultiple(of: 4) // false
```

#### abs

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

## Double

### init

#### random

```swift
Double.random(in: 10.0 ..< 20.0)
```

#### constants

```swift
Double.pi
Double.infinity
Double.nan
```

### calculation

```swift
4.0.squareRoot() // 2
```

```swift
1.5.rounded(.down) // 1.0
1.5.rounded(.up) // 2.0
1.5.rounded(.towardZero) // 1.0
1.5.rounded(.awayFromZero) // 2.0
1.5.rounded(.toNearestOrAwayFromZero) // 2.0

var floar = 1.5
float.round(...)
```

## Range

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

## Global Numeric Functions

```swift
min(...)
max(...)
abs(...)
```

## String

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

### add

```swift
var a = "Hello"
a.append(contentsOf: ", world!")
print(a)
var b = "Hello"
b.insert(contentsOf: ", world!", at: b.endIndex)
print(b)
var c = "Hello"
print(c + ", world!")
```

### replace

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

### split and join

```swift
func split(
    separator: Self.Element,
    maxSplits: Int = Int.max,
    omittingEmptySubsequences: Bool = true
) -> [Self.SubSequence]
func joined(separator: String = "") -> String
```

## Array

### init

```swift
var emptyDoubles: [Double] = []
var emptyFloats: Array<Float> = Array()
var digitCounts = Array(repeating: 0, count: 10)
```

### properties

```swift
// When you need to check whether your collection is empty, use the isEmpty property instead of checking that the count property is equal to zero.
var isEmpty: Bool { get }
var count: Int { get }
```

```swift
func contains(_ element: Self.Element) -> Bool
func contains(where predicate: (Self.Element) throws -> Bool) rethrows -> Bool
func allSatisfy(_ predicate: (Self.Element) throws -> Bool) rethrows -> Bool
```

### index

```swift
var startIndex: Int { get } // always 0
var endIndex: Int { get } // use `..<`

func firstIndex(of element: Self.Element) -> Self.Index?
func lastIndex(of element: Self.Element) -> Self.Index?

func index(of element: Self.Element) -> Self.Index?
```

### element

```swift
var first: Self.Element? { get }
func first(where predicate: (Self.Element) throws -> Bool) rethrows -> Self.Element?

var last: Self.Element? { get }
func last(where predicate: (Self.Element) throws -> Bool) rethrows -> Self.Element?

func randomElement() -> Self.Element?
```

### append and remove

```swift
mutating func append(_ newElement: Element)
mutating func append<S>(contentsOf newElements: S)
mutating func insert<C>(contentsOf newElements: C, at i: Self.Index)
```

```swift
@discardableResult mutating func removeFirst() -> Self.Element
@discardableResult mutating func removeLast() -> Self.Element
mutating func popLast() -> Self.Element?

mutating func removeSubrange(_ bounds: Range<Self.Index>)
mutating func removeAll(where shouldBeRemoved: (Self.Element) throws -> Bool) rethrows
```

### replace

```swift
mutating func replaceSubrange<C>(_ subrange: Range<Int>, with newElements: C)
```

### sort

```swift
mutating func sort(by areInIncreasingOrder: (Self.Element, Self.Element) throws -> Bool) rethrows
func sorted(by areInIncreasingOrder: (Self.Element, Self.Element) throws -> Bool) rethrows -> [Self.Element]
mutating func reverse()
func reversed() -> ReversedCollection<Self>
mutating func shuffle()
func shuffled() -> [Self.Element]
```

### split and join

```swift
func split(
    separator: Self.Element,
    maxSplits: Int = Int.max,
    omittingEmptySubsequences: Bool = true
) -> [Self.SubSequence]
func joined() -> FlattenSequence<Self>
func joined<Separator>(separator: Separator) -> JoinedSequence<Self> where Separator : Sequence, Separator.Element == Self.Element.Element
```

### forEach and map

```swift
// forEach效果和map一样的 只不过不返回；与for-in相比 for-in可以使用break 因为本质上是循环 而forEach可以理解为一个函数调用 与循环无关所以不能使用break
func forEach(_ body: (Self.Element) throws -> Void) rethrows
func map<T>(_ transform: (Self.Element) throws -> T) rethrows -> [T]
// `s.flatMap(transform)` is equivalent to `Array(s.map(transform).joined())`.
func flatMap<SegmentOfResult>(_ transform: (Self.Element) throws -> SegmentOfResult) rethrows -> [SegmentOfResult.Element] where SegmentOfResult : Sequence 
// 将元素中为nil的项去除
func compactMap<ElementOfResult>(_ transform: (Self.Element) throws -> ElementOfResult?) rethrows -> [ElementOfResult]
func filter(_ isIncluded: (Element) throws -> Bool) rethrows -> [Element]
func reduce<Result>(
    _ initialResult: Result,
    _ nextPartialResult: (Result, Self.Element) throws -> Result
) rethrows -> Result
```

example

```swift
let possibleNumbers = ["1", "2", "three", "///4///", "5"]
let mapped: [Int?] = possibleNumbers.map { str in Int(str) } // [1, 2, nil, nil, 5]
let compactMapped: [Int] = possibleNumbers.compactMap { str in Int(str) } // [1, 2, 5]
```

### for-in

```swift
func enumerated() -> EnumeratedSequence<Self>

func stride<T>(
    from start: T,
    to end: T, // to 不包含end; through 包含end
    by stride: T.Stride
) -> StrideTo<T> where T : Strideable

func sequence<T>(
    first: T,
    next: @escaping (T) -> T?
) -> UnfoldFirstSequence<T>

func zip<Sequence1, Sequence2>(
    _ sequence1: Sequence1,
    _ sequence2: Sequence2
) -> Zip2Sequence<Sequence1, Sequence2> where Sequence1 : Sequence, Sequence2 : Sequence
```

example

```swift
for (n, c) in "Swift".enumerated() {
    print("\(n): '\(c)'")
}

for radians in stride(from: 0.0, to: .pi * 2, by: .pi / 2) {
    let degrees = Int(radians * 180 / .pi)
    print("Degrees: \(degrees), radians: \(radians)") // 0, 90, 180, 270
}

for value in sequence(first: 1, next: { $0 * 2 }) {
    // value is 1, then 2, then 4, then 8, etc.
    print(value) // last print 1048576
    if value == 1024 * 1024 { break }
}

let words = ["one", "two", "three", "four"]
let numbers = 1...4
for (word, number) in zip(words, numbers) {
    print("\(word): \(number)")
}
```

## Dictionary

### properties

```swift
dict.keys
dict.values
```

### for-in

```swift
for (key, value) in dict { ... }
```

## Set

### properties

```swift
func contains(_ member: Element) -> Bool

func isSubset(of other: Set<Element>) -> Bool
func isStrictSubset(of other: Set<Element>) -> Bool
func isSuperset(of other: Set<Element>) -> Bool
func isStrictSuperset(of other: Set<Element>) -> Bool
func isDisjoint(with other: Set<Element>) -> Bool
```

```swift
func randomElement() -> Self.Element?
```

### insert and remove

```swift
@discardableResult mutating func insert(_ newMember: Element) -> (inserted: Bool, memberAfterInsert: Element)
@discardableResult mutating func remove(_ member: Element) -> Element?
```

### operation

#### return new set

```swift
func union<S>(_ other: S) -> Set<Element>
func intersection<S>(_ other: S) -> Set<Element>
func symmetricDifference<S>(_ other: S) -> Set<Element>
func subtracting<S>(_ other: S) -> Set<Element>
```

#### modify original set

```swift
mutating func formUnion<S>(_ other: S)
mutating func formIntersection<S>(_ other: S)
mutating func formSymmetricDifference<S>(_ other: S)
mutating func subtract<S>(_ other: S)
```
