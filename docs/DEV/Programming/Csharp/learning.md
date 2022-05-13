---
title: C#学习笔记
---

# C#学习笔记

## 链接整理

- [C# Documentation](https://docs.microsoft.com/en-us/dotnet/csharp/)
    - [Self-guided tutorials](https://docs.microsoft.com/en-us/users/dotnet/collections/yz26f8y64n7k07?WT.mc_id=dotnet-35129-website)
        - Take your first steps with C#
        - Add logic to your applications with C#
        - Work with data in C#
    - Fundamentals
    - Key concepts
    - [Reference](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/)
- [Tutorial: Create a .NET console application using Visual Studio Code](https://docs.microsoft.com/en-us/dotnet/core/tutorials/with-visual-studio-code?pivots=dotnet-6-0)

## Take your first steps with C#

```csharp
Console.WriteLine("Hello World!");
Console.Write("Hello World!");
```

## Tutorial: Create a .NET console application using Visual Studio Code

```
$ mkdir <folder>
$ cd <folder>
$ dotnet new console --framework net6.0
$ code .

$ dotnet run
```

使用英文：

```
$ vim ~/.zshrc

# .NET
set DOTNET_CLI_UI_LANGUAGE="en-US"
export DOTNET_CLI_UI_LANGUAGE="en-US"
export LANG=en_US.UTF-8
```

## Add logic to your applications with C#

- `string.Trim()`
- `string.ToLower()`
- `string.ToUpper()`
- `string.Contains`
- 有问号冒号表达式
- 用`$`加双引号后用大括号表示表达式

```cs
int saleAmount = 1001;
Console.WriteLine($"Discount: {(saleAmount > 1000 ? 100 : 50)}");
```

## Work with data in C#

- signed integral types: `sbyte` `short` `int` `long`
- unsigned integral types: `byte` `ushort` `uint` `ulong`
- 小数: `float`(f/F) `double`(d/D/不加) 需要十进制的精度 `decimal`(m/M)（一般用double完全够）
- `int[] data;`
- `int[] data = new int[3];`
