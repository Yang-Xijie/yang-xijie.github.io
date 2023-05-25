# 应对 OJ 系统的策略

> 201009 绕淙元学长(rls)数算OJ小班辅导笔记
> 
> OJ网址[lambdaoj.com](http://lambdaoj.com/)

## 判题结果

- COMPILE_ERROR(CE): 编译出错了，代码本身的问题
- BAD_SYSCALL: 使用了非法的系统调用，要么是恶意代码，大部分情况是C++在new一块内存的时候，超过了限制失败了，C++运行时环境需要一个系统调用关闭信号，然后杀死这个进程。或者`assert()`
- RUN_TIME_ERROR(RE): 运行时错误，可能是由于除零、引用空指针或者数组越界等等
- TIME_LIMIT_EXCEEDED(TLE): 程序超时，可能是死循环，也可能是算法不够优，或者实现不够优, 还没到核对答案那一步，内存情况也不明
- MEMORY_LIMIT_EXCEEDED(MLE): 程序超过内存限制，可能是算法不够优，或者实现不够优，也没有到核对答案那一步
- WRONG_ANSWER(WA): 程序正常执行，也没有超时和超内存，但是答案不对
- ACCEPTED(AC): 结果完全正确

## 输入和输出

输入与输出是两个互不干扰的流，你可以在还没读完数据的情况下进行输出

## stdio.h和iostream

最好使用`<cstdio>`，一方面是它自身经过编译占内存（700KB左右）比`<iostream>`（1.3MB左右）小；而是读入/输出数据很快；三是数据读入/输出格式化很方便。

## 快读

想比`scanf()`更快，可以用`fgets()`裸读字符串，读入之后自己对字符串进行处理

如此提前优化的原因是：你比计算机知道得多一些

```cpp
// 逐行读入整数
int quickRead() {
  char s[16];
  fgets(s, 16, stdin);
  int result = 0;
  char *p = s;
  while (*p >= '0' && *p <= '9') {
    result *= 10;
    result += *p - '0';
    p++;
  }
  return result;
}
```

## new和delete

如果非必要，不要用`new`（因为其本身存在缺陷，浪费时间和空间），也不要用`delete`；内存稳定的写法是直接按题目中最大数据的规模开数组

## 内存和时间限制

直接考虑最大（最后一个点）的数据量就好了

## 重定向

自己验证数据时可以灵活运用重定向来方便自己debug

### 例

输入若干字符串，输入格式为一行一个

对这些字符串原样输出

注：`scanf()`会返回成功读入的数据项数，读入数据时遇到了“文件结束”或遇到了错误则返回`EOF`

#### 直接在终端输入和输出

```cpp
///直接在终端输入和输出
#include <iostream>
using namespace std;

int main() {
  char c[1000][128];
  int i = 0;
  while (scanf("%s", c[i]) != EOF) i++;
  // 在Mac或Linux上若在终端输入可以用⌃D结束输入
  // 在Windows上若在终端输入可以用⌃Z结束输入
  for (int j = 0; j <= i - 1; j++) printf("%s\n", c[j]);
}
```

#### 从文件读入或向文件输出

```cpp
///从文件读入或向文件输出
#include <iostream>
using namespace std;

int main() {
  char c[1000][128];
  int i = 0;
  freopen("./input.txt", "r", stdin);
  // 将stdin重定向到已经写好的输入数据input.txt中
  freopen("./output.txt", "w", stdout);
  // 这里的路径你可以写绝对路径；如果要写相对路径那要知道当前命令是在哪里执行的
  while (scanf("%s", c[i]) != EOF) i++;
  for (int j = 0; j <= i - 1; j++) printf("%s\n", c[j]);
}
```

#### 通过命令行进行重定向

在macOS或Linux下，编译如下代码生成可执行文件之后（如redirection.out），在终端执行`./redirection.out < input.txt > output.txt`即可执行该`.out`文件并进行重定向

```cpp
#include <iostream>
using namespace std;

int main() {
  char c[1000][128];
  int i = 0;
  while (scanf("%s", c[i]) != EOF) i++;
  for (int j = 0; j <= i - 1; j++) printf("%s\n", c[j]);
}
```

##  STL

`vector`可以取代数组

`stack` `queue`都很常用

`map` `unordered_map` `set`以后应该会用到

算法库`algorithm`里面有一些很好用的东西，比如排序

### 例

用vector构建一个数组，采用三种方法将其输出三次

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
  vector<int> s;
  s.push_back(1);
  s.push_back(2);
  s.push_back(3);
  for (int i = 0; i <= (int)s.size() - 1; i++) {
    cout << s[i] << endl;
  }
  for (auto it = s.begin(); it != s.end(); it++) {
    cout << *it << endl;
  }
  for (auto &i : s) {
    cout << i << endl;
  }
}
```

## assert()

`assert()` 传入参数为true则什么都不发生，为false则会Bad Syscall

```cpp
#include <cassert>
#include <cstdio>
const int guessScale = 500000;
int main() {
  int m, n, k, l;
  std::scanf("%d%d%d%d", &m, &n, &k, &l);
  assert(m + n + k + l <= guessScale);
}
// 当guessScale逐渐增大到50w时，最后一个点的
// Bad Syscall消失，这说明数据规模不会超过50w
```

## 大气一点

开数组、字符串的时候可以大气一点。这是说开长度为100的数组直接开成128的，开500的直接开成512的，开20w就开200001或者更大。这样可能会避免自己一些愚蠢的错误。

## OJ解题步骤

- 考虑数据结构（画图确定）
- 考虑算法（分析复杂度）
- 实现（用C++代码写出来）

# 寻找丢失的筷子

## 问题描述

小明买了N对筷子，每对筷子由两只长度相同的筷子组成，不同对筷子的长度也可能相同。每只筷子长度均为正整数。一天，马虎的小明丢失了一只筷子， 只剩下（2N-1）只筷子，他想知道丢失的筷子的长度是多少？

## 输入格式

第一行一个整数N，表示筷子的对数。

接下来2N-1行，每行一个整数，依次表示剩下2N-1只筷子的长度。

## 输出格式

一个整数，表示丢失筷子的长度。

## 输入样例

```
3
2
3
3
2
3
```

## 输出样例

```
3
```

## 代码实现

```cpp
#include <cstdio>
using namespace std;

int main() {
  int n, temp, result = 0;
  scanf("%d", &n);
  for (int i = 0; i <= 2 * n - 2; i++) {
    scanf("%d", &temp);
    result ^= temp;
  }
  printf("%d\n", result);
}
```
