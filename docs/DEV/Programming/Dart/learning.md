# Dart 学习笔记

> https://dart.dev/guides/language/language-tour

## A basic Dart program

```dart
// Define a function.
void printInteger(int aNumber) {
  print('The number is $aNumber.'); // Print to console.
}

// This is where the app starts executing.
void main() {
  var number = 42; // Declare and initialize a variable.
  printInteger(number); // Call a function.
}
```

- string literal - `'xxx'` or `"xxx"`
- string interpolation - `$variable` or `${variable}`

## Important concepts

- Everything you can place in a variable is an object, and every object is an instance of a class.
- all objects inherit from the Object class.
- Dart is strongly typed
- You can make a variable nullable by putting a question mark (?) at the end of its type. For example, a variable of type int? might be an integer, or it might be null.
- If you enable null safety, variables can’t contain null unless you say they can.
- `null` is an object
- Dart supports generic types, like `List<int>`
- If an identifier starts with an underscore (_), it’s private to its library.

## Variables

```Dart
var name = 'Bob'; // 类型推断
Object name = 'Bob'; // 相当于弱类型
String name = 'Bob'; // 指明类型
```

- Production code ignores the assert() call.

```dart
late String description;

void main() {
  description = 'Feijoada!';
  print(description);
}
```

- A `final` variable can be set only once.
- A `const` variable is a compile-time constant. (Const variables are implicitly final.)
- Instance variables can be final but not const.
- You can also use `const` to create constant values.
- Although a final object cannot be modified, its fields can be changed. In comparison, a const object and its fields cannot be changed: they’re immutable.

## Built-in types

- Numbers (`int`, `double`)
- Strings (`String`)
- Booleans (`bool`)
- Lists (`List`, also known as arrays)
- Sets (`Set`)
- Maps (`Map`)
- Runes (`Runes`; often replaced by the characters API)
- Symbols (`Symbol`)
- The value null (`Null`)

---

- `Object`: The superclass of all Dart classes except Null.
- `Enum`: The superclass of all enums.
- `Future` and `Stream`: Used in asynchrony support.
- `Iterable`: Used in for-in loops and in synchronous generator functions.
- `Never`: Indicates that an expression can never successfully finish evaluating. Most often used for functions that always throw an exception.
- `dynamic`: Indicates that you want to disable static checking. Usually you should use Object or Object? instead.
- `void`: Indicates that a value is never used. Often used as a return type.

To get the string corresponding to an object, Dart calls the object’s `toString()` method.

```dart
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a
multi-line string.""";

var s = r'In a raw string, not even \n gets special treatment.';
```

spread operator (`...`):

```dart
var list = [1, 2, 3];
var list2 = [0, ...list];
assert(list2.length == 4);
```

```dart
var listOfInts = [1, 2, 3];
var listOfStrings = ['#0', for (var i in listOfInts) '#$i'];
assert(listOfStrings[1] == '#1');
```

```dart
Set<String> names = {}; // This works, too.
```

## Functions

Dart is a true object-oriented language, so even functions are objects and have a type, `Function`.

When defining a function, use `{param1, param2, ...}` to specify named parameters.

```dart
void enableFlags({bool bold = false, bool hidden = false}) {...}
```

The `main()` function returns void and has an optional `List<String>` parameter for arguments.

```dart
// Run the app like this: dart args.dart 1 test
void main(List<String> arguments) {
  print(arguments);

  assert(arguments.length == 2);
  assert(int.parse(arguments[0]) == 1);
  assert(arguments[1] == 'test');
}
```

[args lib](https://pub.dev/packages/args)

函数作为变量：

```dart
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```

匿名函数：

```dart
const list = ['apples', 'bananas', 'oranges'];
list.forEach((item) {
  print('${list.indexOf(item)}: $item');
});
```

All functions return a value. If no return value is specified, the statement return null; is implicitly appended to the function body.

## Operators

```dart
assert(5 / 2 == 2.5); // Result is a double
assert(5 ~/ 2 == 2); // Result is an int
```

- Type test operators
    - `as` Typecast
    - `is` True if the object has the specified type
    - `is!` True if the object doesn’t have the specified type

`condition ? expr1 : expr2` `expr1 ?? expr2`

Cascade notation

```dart
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;

querySelector('#confirm') // Get an object.
  ?..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'))
  ..scrollIntoView();
```

```dart
var message = StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  message.write('!');
}

var collection = [1, 2, 3];
collection.forEach(print); // 1 2 3
```

`switch-case` 需要有 `break`。

## Classes

Use a type test operator rather than `runtimeType` to test an object’s type. In production environments, the test `object is Type` is more stable than the test `object.runtimeType == Type`.

构造函数：

```dart
class Point {
  double x = 0;
  double y = 0;

  Point(double x, double y) {
    // See initializing formal parameters for a better way
    // to initialize instance variables.
    this.x = x;
    this.y = y;
  }
}
```

Use `this` only when there is a name conflict. Otherwise, Dart style omits the `this`.

```dart
class Rectangle {
  double left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // Define two calculated properties: right and bottom.
  double get right => left + width;
  set right(double value) => left = value - width;
  double get bottom => top + height;
  set bottom(double value) => top = value - height;
}

void main() {
  var rect = Rectangle(3, 4, 20, 15);
  assert(rect.left == 3);
  rect.right = 12;
  assert(rect.left == -8);
}
```

Adding features to a class: mixins

```dart
class Musician extends Performer with Musical {
  // ···
}

class Maestro extends Person with Musical, Aggressive, Demented {
  Maestro(String maestroName) {
    name = maestroName;
    canConduct = true;
  }
}
```

## Libraries

```dart
import 'dart:html';
import 'package:test/test.dart';
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;
import 'package:lib1/lib1.dart' show foo;
import 'package:lib2/lib2.dart' hide foo;
```

## Typedefs

```dart
typedef IntList = List<int>;
IntList il = [1, 2, 3];
```
