# Swift 笔记 ｜ 基础语法

> - [A Swift Tour](https://docs.swift.org/swift-book/GuidedTour/GuidedTour.html)
> - [The Basics](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)

## Simple Values

- `var` `let`
- `: Type`
- Values are never implicitly converted to another type. If you need to convert a value to a different type, explicitly make an instance of the desired type.
- `"\(...)"`
- `"""..."""`
- Array `[Int]` `[1, 2, 3]` `[]`
- Dictionary `[String: Int]` `["1": 1, "2": 2, "3": 3]` `[:]`

## Control Flow

- `for element in array { ... }`
- `if ...` `else if ...`
- `: Type?` `nil` `!` `??` `if let`
- `switch ... { case A: ... case B: ... default: ... }`
- `while ... { ... }` `repeat { ... } while ...`
- `..<` `...`

## Functions and Closures

- `func FuncName(inside outside: Type) -> Type { return ... }`
    - `inside` be `_`
- Tuple `(name: Type, name: Type)`
- Functions can be nested.
- Functions are a first-class type. This means that a function can return another function as its value. A function can take another function as one of its arguments.
- `{ (number: Int) -> Int in ...}`
- `numbers.sorted { $0 > $1 }`

## Objects and Classes

- `init()`
- `class Son: Futher` `override`
- var `get { ... } set { ... }` `willSet { ... } didSet { ... }`

## Enumerations and Structures

enum

- `enum EnumName: Type`
- `init?(rawValue:)`

struct

- One of the most important differences between structures and classes is that structures are always copied when they’re passed around in your code, but classes are passed by reference.

## Concurrency

同步(Synchronous) 异步(Asynchronous)

Use `async` to mark a function that runs asynchronously.

```swift
func fetchUserID(from server: String) async -> Int {
    if server == "primary" {
        return 97
    }
    return 501
}
```

You mark a call to an asynchronous function by writing await in front of it.

```swift
func fetchUsername(from server: String) async -> String {
    let userID = await fetchUserID(from: server)
    if userID == 501 {
        return "John Appleseed"
    }
    return "Guest"
}
```

Use `async let` to call an asynchronous function, letting it run in parallel with other asynchronous code. When you use the value it returns, write `await`.

```swift
func connectUser(to server: String) async {
    async let userID = fetchUserID(from: server)
    async let username = fetchUsername(from: server)
    let greeting = await "Hello \(username), user ID \(userID)"
    print(greeting)
}
```

Use `Task` to call asynchronous functions from synchronous code, without waiting for them to return.

```swift
Task {
    await connectUser(to: "primary")
}
// Prints "Hello Guest, user ID 97"
```

## Protocols and Extensions

- `protocol ExampleProtocol { ... }`
- `class SimpleClass: ExampleProtocol { ... }`
- `extension Int: ExampleProtocol { ... }`

## Error Handling

- `enum PrinterError: Error { ... }`
- `func FuncName( ... ) throws { ... }`
- `do { ... try ... } catch { print(error) }` `catch let printerError as PrinterError { ...}`
- `try?` `try!`
- Use defer to write a block of code that’s executed after all other code in the function, just before the function returns. `defer { ... }`

## Generics

- `func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] { ... }`
- `func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool where T.Element: Equatable, T.Element == U.Element { ... }`

```swift
// Reimplement the Swift standard library's optional type
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var possibleInteger: OptionalValue<Int> = .none
possibleInteger = .some(100)
```
