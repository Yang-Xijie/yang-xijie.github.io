# C++ 实例 | 栈类模版

```cpp
#include <stdlib.h>

#include <iostream>
using namespace std;

// 栈的类模板
template <class T>
class Stack {
 public:
  Stack(int size);
  Stack(const Stack &p);
  virtual ~Stack();
  void Push(const T &e);
  const T &Pop();
  const T &Peek() const;
  bool IsEmpty() const;

 private:
  T *buff;
  int max;
  int top;  //当前数据所在的地方(相当于一个标记)
};

// 栈类模板的构造函数模板: 给过来栈的空间新建一个栈对象/实例化栈对象,
// 其中数据的数据类型是T
template <class T>
Stack<T>::Stack(int size) {
  buff = new T[max = size];
  top = -1;  // 刚刚开始还没存数据呢
}

// 栈类模板的复制构造函数模板: 给定一个已经实例化的栈对象,
// 用这一栈类复制构造一个实例化栈对象
template <class T>
Stack<T>::Stack(const Stack &p) {
  buff = new T[max = p.max];
  top = p.top;
  for (int i = 0; i <= top; i++) buff[i] = p.buff[i];  //把数据挨个复制过来
}

// 栈类模板的析构函数模板
template <class T>
Stack<T>::~Stack() {
  delete[] buff;  //其他东西程序会自己析构掉, 不过带[]的delete要自己写的
}

// 入栈操作函数模板
template <class T>
void Stack<T>::Push(const T &e) {
  if (top >= max - 1)
    cout << "overflow!" << endl;
  else
    buff[++top] = e;
}

// 出栈操作函数模板
template <class T>
const T &Stack<T>::Pop() {
  if (top < 0) {
    cout << "underflow!" << endl;
    return buff[0];  // 老师: 这个返回值没有意义,仅为了通过编译; 我:
                     // vscode上注释掉可以通过编译
  } else
    return buff[top--];
}

// 读栈顶元素函数模板
template <class T>
const T &Stack<T>::Peek() const {
  if (top < 0) {
    cout << "underflow!" << endl;
    return buff[0];  // 这个返回值没有意义,仅为了通过编译
  } else
    return buff[top];
}

// 判断栈是否为空函数模板
template <class T>
bool Stack<T>::IsEmpty() const {
  return top < 0;
}

int main() {
  Stack<double> DoubleStack(
      10);  //创建了一个名为DoubleStack的最多可以存储10个duoble数据的栈对象
            // T= double, size=10
  Stack<int> IntStack(
      15);  //创建了一个名为IntStack的最多可以存储15个int数据的栈对象
            // T= int, size=15

  //填数据
  for (double i = 1.0; i <= 20.0; i += 2.0) DoubleStack.Push(i);
  for (int j = 0; j < 75; j += 5) IntStack.Push(j);

  //在出栈之前复制, 并出栈
  Stack<double> DoubleStack2(DoubleStack);  // 复制
  while (!DoubleStack2.IsEmpty()) cout << DoubleStack2.Pop() << " ";
  cout << endl;
  Stack<int> IntStack2(IntStack);  // 复制
  while (!IntStack2.IsEmpty()) cout << IntStack2.Pop() << " ";
  cout << endl;

  //最开始的两个栈对象现在出栈
  while (!DoubleStack.IsEmpty()) cout << DoubleStack.Pop() << " ";
  cout << endl;
  while (!IntStack.IsEmpty()) cout << IntStack.Pop() << " ";
  cout << endl;

  //这里会自己析构掉

  system("pause");
}
```
