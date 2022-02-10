# Xcode 新建开发模块

## 背景

开发app的时候，最终发布的应用只会有一个。但是在实际编写app的过程中，我们经常需要有一个测试版app。

## 步骤

〇 1 添加一个`Build Configuration`
`Project` -> `Info` -> `Configurations` -> `+` -> `Dev`

〇 2 新建Scheme，并使用刚刚建好的`Build Configuration`
`Product` -> `Scheme` -> `New Scheme...`
`Edit` -> `Run/Test/Analyze` -> `Info` -> `Build Configuration `-> `Dev`

〇 3 添加Swift编译flag，以支持在代码中使用条件编译
 `PROJECT` -> `Build Settings` -> `Swift Compiler` - `Custom Flags` -> `Other Swift Flags` ->` Dev` 添加`-DDEV` (use `#if DEV` `#endif` )

〇 4 (Optioinal) 修改测试版app的ID，这样在虚拟机上测试的时候就可以同时有两种不同Build Configuration的app
`Project` -> `Targets` -> `Build Configuration` -> `Packaging` -> `Product Bundle Identifier` -> `Dev` append `.dev`

〇 5 (Optioinal) 修改app名称
`Project` -> `Targets` -> `Build Configuration` -> `Packaging` -> `Product Name` -> set `Debug/Dev/Release`

## -DDEV

[Bilibili |【Swift】swiftc -D参数 使用指南](https://www.bilibili.com/video/BV1Au41197qG)

```sh
$ swiftc --help | grep -- -D
-D <value>    Marks a conditional compilation flag as true
```

```
$ vim hello.swift
```

```swift
#if DEV
print("Hello, developer!")
#else
print("Hello!")
#endif
```

```sh
$ swiftc hello.swift
$ ./hello
Hello!

$ swiftc hello.swift -DDEV
$ ./hello
Hello, developer!
```
