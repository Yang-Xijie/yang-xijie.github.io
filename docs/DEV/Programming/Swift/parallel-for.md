# Swift | Parallel

在我们使用for循环的时候，其中的语句总是在前一个for完成之后才执行下一个。当执行大批量任务时，如果其中的任务相互独立，可以使用`DispatchQueue.concurrentPerform`来使用多线程平行的同步执行这些任务来节省时间。

```swift
// main.swift

import Foundation

let start = CFAbsoluteTimeGetCurrent()

var array = [Int](repeating: 0, count: 60_000_000)

// 60_000_000 30s
// for i in 0 ... array.count - 1 {
//    array[i] = i
// }

// 60_000_000 1.7s
DispatchQueue.concurrentPerform(iterations: array.count) { i in
    array[i] = i
}

let diff = CFAbsoluteTimeGetCurrent() - start
print("[Took \(diff) seconds]")
```

References:

- <https://www.advancedswift.com/parallel-for-loops-in-swift/>
- <https://developer.apple.com/documentation/dispatch/dispatchqueue/2016088-concurrentperform>
