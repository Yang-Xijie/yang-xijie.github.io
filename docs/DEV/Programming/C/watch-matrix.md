# C 二维数组调试

## 一维数组

一维数组在调试器中是可以直接显示的 本质上变量`x`是一个指针 指向数组对应的第一个元素

```c
/* 输入一个一维数组 从低到高排序 */

#include <stdio.h>

#define DEBUG  // 不希望有自己debug的输出语句把这一行注释掉

#ifdef DEBUG
void printArray(int *x, int N) {
  printf("Array: ");
  for (int i = 0; i < N; i++) {
    printf("%d ", x[i]);
  }
  printf("\n");
}
#endif

int main() {
  freopen("./input.txt", "r", stdin);
  // input.txt
  // 6
  // 6 5 4 3 2 1

  int N = 0;
  printf("请输入数组长度: ");
  scanf("%d", &N);
  printf("\n");

  int x[N];
  // 输入
  for (int i = 0; i < N; i++) {
    printf("请输入第%d个元素的值: ", i);
    scanf("%d", &x[i]);
    printf("\n");
  }

  printf("开始排序\n");
  for (int epoch = 0; epoch < N; epoch++) {
    for (int i = 0; i < N - 1 - epoch; i++) {
      if (x[i] > x[i + 1]) {
        int temp = x[i];
        x[i] = x[i + 1];
        x[i + 1] = temp;
      }
#ifdef DEBUG
      printArray(x, N);
#endif
    }
  }
}
```

Output:

```
请输入数组长度: 
请输入第0个元素的值: 
请输入第1个元素的值: 
请输入第2个元素的值: 
请输入第3个元素的值: 
请输入第4个元素的值: 
请输入第5个元素的值: 
开始排序
Array: 5 6 4 3 2 1 
Array: 5 4 6 3 2 1 
Array: 5 4 3 6 2 1 
Array: 5 4 3 2 6 1 
Array: 5 4 3 2 1 6 
Array: 4 5 3 2 1 6 
Array: 4 3 5 2 1 6 
Array: 4 3 2 5 1 6 
Array: 4 3 2 1 5 6 
Array: 3 4 2 1 5 6 
Array: 3 2 4 1 5 6 
Array: 3 2 1 4 5 6 
Array: 2 3 1 4 5 6 
Array: 2 1 3 4 5 6 
Array: 1 2 3 4 5 6
```

## 二维数组

二维数组具体实现我并不清楚 以前好像说过要尽量避免使用二维数组 坑比较多

一定要用的话，传参可以通过如下两种比较直观的方式

```c
/* 打印二维数组 */

#include <stdio.h>

// 将二维数组转换为一维传入即可
void printMatrix1(int *A, int r, int c) {
  for (int i = 0; i <= r - 1; i++) {
    for (int j = 0; j <= c - 1; j++) {
      printf("%d ", A[i * c + j]);
    }
    printf("\n");
  }
}

// 按照符合直觉的二维数组传入参数 C99开始支持
void printMatrix2(int r, int c, int A[r][c]) {
  for (int i = 0; i <= r - 1; i++) {
    for (int j = 0; j <= c - 1; j++) {
      printf("%d ", A[i][j]);
    }
    printf("\n");
  }
}

int main() {
  int r = 3;
  int c = 4;
  int A[r][c];
  for (int i = 0; i <= r - 1; i++) {
    for (int j = 0; j <= c - 1; j++) {
      A[i][j] = i * c + j;
    }
  }

  printf("printMatrix1()\n");
  printMatrix1(*A, r, c);
  printf("printMatrix2()\n");
  printMatrix2(r, c, A);
}
```

Output:

```
printMatrix1()
0 1 2 3 
4 5 6 7 
8 9 10 11 
printMatrix2()
0 1 2 3 
4 5 6 7 
8 9 10 11
```

### 调试二维数组

二维数组本质上也是一个指针指向数组第一行的第一个元素 但是可能由于编译器编译时去掉了长度信息（或者本来就没有） 所以需要在调试时手动指定如何读取该指针处的结构体

在这个例子里面 使用 `*(int(*)[3][4])A` 这样的表达式来做一次转换就可以了

- Xcode > 调试开始后的变量窗口 > 右键 > Add Expression...
- VS Code > 调试开始后的变量窗口下方的Watch窗口 > 加号

### lldb调试过程

```
(lldb) breakpoint set -f test.c -l 34
Breakpoint 1: where = hello-debug`main + 232 at test.c:35:3, address = 0x0000000100003ed8
(lldb) run
Process 46066 launched: '/Users/yangxijie/Downloads/__TEMP/C-debug-try/build/hello-debug' (x86_64)
Process 46066 stopped
* thread #1, queue = 'com.apple.main-thread', stop reason = breakpoint 1.1
    frame #0: 0x0000000100003ed8 hello-debug`main at test.c:35:3
   32       }
   33     }
   34  
-> 35     printf("printMatrix1()\n");
   36     printMatrix1(*A, r, c);
   37     printf("printMatrix2()\n");
   38     printMatrix2(r, c, A);
Target 0: (hello-debug) stopped.
(lldb) frame variable
(int) r = 3
(int) c = 4
(int [][]) A = ([0] = int [] @ 0x00007ff7bfeff280, [1] = int [] @ 0x00007ff7bfeff284, [2] = int [] @ 0x00007ff7bfeff288, [3] = int [] @ 0x00007ff7bfeff28c)
(lldb) frame variable A
(int [][]) A = ([0] = int [] @ 0x00007ff7bfeff280, [1] = int [] @ 0x00007ff7bfeff284, [2] = int [] @ 0x00007ff7bfeff288, [3] = int [] @ 0x00007ff7bfeff28c)
(lldb) expr *(int(*)[3])A
(int [3]) $0 = ([0] = 0, [1] = 1, [2] = 2)
(lldb) expr *(int(*)[8])A
(int [8]) $1 = ([0] = 0, [1] = 1, [2] = 2, [3] = 3, [4] = 4, [5] = 5, [6] = 6, [7] = 7)
(lldb) expr *(int(*)[12])A
(int [12]) $2 = ([0] = 0, [1] = 1, [2] = 2, [3] = 3, [4] = 4, [5] = 5, [6] = 6, [7] = 7, [8] = 8, [9] = 9, [10] = 10, [11] = 11)
(lldb) expr *(int(*)[3][4])A
(int [3][4]) $3 = {
  [0] = ([0] = 0, [1] = 1, [2] = 2, [3] = 3)
  [1] = ([0] = 4, [1] = 5, [2] = 6, [3] = 7)
  [2] = ([0] = 8, [1] = 9, [2] = 10, [3] = 11)
}
```

可以看到 用 `frame variable A` 只能看到第一行的数据，我们需要手动通过表达式做转化

## References

- https://blog.csdn.net/weixin_42033845/article/details/107921889
- https://blog.csdn.net/Kobe51920/article/details/90739757
- https://github.com/Microsoft/vscode-cpptools/issues/172#issuecomment-280520910
- https://lldb.llvm.org/use/tutorial.html
- https://github.com/Yang-Xijie/C-Makefile-template
