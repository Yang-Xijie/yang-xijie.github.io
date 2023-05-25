# stdout 按行缓冲

在macOS上使用下面的命令执行程序，分别查看三个函数的运行结果

```
gcc a.c -o a && ./a
```

```c
#include <stdio.h>
#include <stdlib.h>

void func0() {
  printf("first");
  system("clear");
  printf("second");
}  // 输出 firstsecond% // 注 `%`是指该位置没有换行符

void func1() {
  printf("first");
  fflush(stdout);  // 现在就输出缓冲区的内容
  system("clear");
  printf("second");
}  // 输出 second%

void func2() {
  printf("first\n");
  // 推测 在`printf()`中加`\n` 和 用 `fflush(stdout);` 的作用一致
  // 我就上Stack Overflow查了一下
  // https://stackoverflow.com/questions/1716296/why-does-printf-not-flush-after-the-call-unless-a-newline-is-in-the-format-strin
  // 给出的解释是`printf()`是按照行缓冲的 也就是攒够一行才会向控制台输出
  // 这大致是因为输出是比较耗时耗资源的事情 所以尽量减少输出的调用次数 就做了这样的设计
  system("clear");
  printf("second");
}  // 输出 second%

int main() {
  func0();
  // func1();
  // func2();
  return 0;
}
```
