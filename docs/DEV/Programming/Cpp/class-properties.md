# C++ 笔记 | 类数据成员 const static

> 类：成员，常成员，静态成员，常静态成员搞不懂；举了个例子终于搞清楚了
> 
> 踩了不少坑

## 代码

```cpp
#include <stdio.h>
#include <stdlib.h>

#include <iostream>
using namespace std;

class Student {
 public:
  /* 每个对象都会有一个的数据成员 */
  int age_;
  const int kGender;  // const确保一经赋值不会被修改
                      // true 男 false 女

  /* static 所有类对象共用一个常量数据成员 */
  static int kCount;  // 所有类对象共用的一个数据, 若不在类外赋值则无法使用
                      // 有const就无法修改
  const static int kSchool;  // #1
  // 假如说学生都是一个学校的,学校代码是123,学生不转学
  // const static int kSchool = 123;  // 等同于 #1+#2
  // 一个变量只有拥有类外定义的情况下，才能被获得地址。下面kPi同
  // 因此这种写法不会被允许在后面被打印出地址
  // 真的不会, 将(int*)变为(int* const)都不会
  const static double kPi;  // #3
  // constexpr static double kPi = 3.14159; // 等同于 #3+#4

 public:
  Student(int age = 18, const bool gender = true) : age_(age), kGender(gender) {
    kCount++;
  }
};

int Student::kCount = 0;  // 若不在类外赋值则无法使用
                          //而且必须这么做, 不像常量int类还可以放在类内赋值
const int Student::kSchool = 123;     // #2
const double Student::kPi = 3.14159;  // #4

int main() {
  // cout << Student.age_ << endl;     //不允许使用类名调用数据
  // cout << Student.kGender << endl;  //不允许使用类名调用数据
  // cout << Student.kCount << endl;   //不允许使用类名调用数据
  // cout << Student.kSchool << endl;  //不允许使用类名调用数据
  // cout << Student.kPi << endl;      //不允许使用类名调用数据
  // 同样不可以使用类名调用函数

  // cout << Student::age_ << endl;     //只有对象才有非静态成员
  // cout << Student::kGender << endl;  //只有对象才有非静态成员
  cout << "Student::kCount\t" << Student::kCount << endl;
  cout << "Student::kPi\t" << Student::kPi << endl;
  cout << "Student::kSchool\t" << Student::kSchool << endl;
  cout << endl << endl;

  Student s1(19, true);
  cout << "s1.age_\t" << s1.age_ << endl;
  cout << "s1.kGender\t" << s1.kGender << endl;
  cout << "s1.kCount\t" << s1.kCount << endl;
  cout << "s1.kSchool\t" << s1.kSchool << endl;
  cout << "s1.kPi\t" << s1.kPi << endl;
  cout << endl;

  Student s2(17, false);
  cout << "s2.age_\t" << s2.age_ << endl;
  cout << "s2.kGender\t" << s2.kGender << endl;
  cout << "s2.kCount\t" << s2.kCount << endl;
  cout << "s2.kSchool\t" << s2.kSchool << endl;
  cout << "s2.kPi\t" << s2.kPi << endl;
  cout << endl << endl;

  printf("&s1.age_\t%p\n", &s1.age_);
  printf("&s2.age_\t%p\n", &s2.age_);
  cout << endl;

  printf("&s1.kGender\t%p\n", &s1.kGender);
  printf("&s2.kGender\t%p\n", &s2.kGender);
  cout << endl;

  printf("&s1.kCount\t%p\n", &s1.kCount);
  printf("&s2.kCount\t%p\n", &s2.kCount);
  printf("&Student::kCount\t%p\n", &Student::kCount);
  cout << endl;

  printf("&s1.kSchool\t%p\n", &s1.kSchool);
  printf("&s2.kSchool\t%p\n", &s2.kSchool);
  printf("&Student::kSchool\t%p\n", &Student::kSchool);
  cout << endl;

  printf("&s1.kPi\t%p\n", &s1.kPi);
  printf("&s2.kPi\t%p\n", &s2.kPi);
  printf("&Student::kPi\t%p\n", &Student::kPi);
  cout << endl << endl;

  cout << "&s1.age_\t" << (int*)&s1.age_ << endl;
  cout << "&s2.age_\t" << (int*)&s2.age_ << endl;
  cout << endl;
  cout << "&s1.kGender\t" << (int*)&s1.kGender << endl;
  cout << "&s2.kGender\t" << (int*)&s2.kGender << endl;
  cout << endl;

  cout << "&s1.kCount\t" << (int*)&s1.kCount << endl;
  cout << "&s2.kCount\t" << (int*)&s2.kCount << endl;
  cout << "&Student::kCount\t" << (int*)&Student::kCount << endl;
  cout << endl;

  cout << "&s1.kSchool\t" << (int*)&s1.kSchool << endl;
  cout << "&s2.kSchool\t" << (int*)&s2.kSchool << endl;
  cout << "&Student::kSchool\t" << (int*)&Student::kSchool << endl;
  cout << endl;

  cout << "&s1.kPi\t" << (int*)&s1.kPi << endl;
  cout << "&s2.kPi\t" << (int*)&s2.kPi << endl;
  cout << "&Student::kPi\t" << (int*)&Student::kPi << endl;
  cout << endl;

  system("pause");
}
/*
  const static 和 static const一样，
  都不能在类内直接初始化非整形常量，
  可以修饰int，bool，char，
  但不能修饰其他类型（如double，float）
  在c++11中，可以使用 constexpr static 或者 static constexpr
  来修饰非整形静态成员常量
  ----
  为什么标准不允许这一行为？
  Bjarne这样解释：
  一个类会被特别定义在一个头文件中，并且头文件会被包含在许多转换单元里。
  但是，为了防止链接规则过于复杂，C++需要每一个对象有特定的定义。
  如果C++允许存储在内存中的对象进行类内定义，那么这一规则将会被打破。
  ----
  为什么只有static const integral类型以及enums被允许类内初始化呢？
  这个答案就在Bjarne的那段话中。“C++需要每一个对象有特定的定义。
  如果C++允许存储在内存中的对象进行类内定义，那么这一规则将会被打破。”

  注意只有static const integers 会被看作编译时的常量。
  编译器了解这样的integer在任何情况下都不会改变，
  因此编译器才可以对其做出特有的优化与改进，编译器会简单的将其内联化这样的变量，
  因而不再使其保存在内存中。因为保存在内存中的需求被移除了，使得他们成了Bjane所说规则的例外。

  值得注意的是，即使static const
  integral这样的变量被允许使用类内初始化，但是获取这样的变量的地址是不被允许的。
  一个变量只有拥有类外定义的情况下，才能被获得地址。
*/
```

## 结果

```
Student::kCount 0
Student::kPi    3.14159
Student::kSchool        123


s1.age_ 19
s1.kGender      1
s1.kCount       1
s1.kSchool      123
s1.kPi  3.14159

s2.age_ 17
s2.kGender      0
s2.kCount       2
s2.kSchool      123
s2.kPi  3.14159


&s1.age_        000000000061FE18
&s2.age_        000000000061FE10

&s1.kGender     000000000061FE1C
&s2.kGender     000000000061FE14

&s1.kCount      0000000000408030
&s2.kCount      0000000000408030
&Student::kCount        0000000000408030

&s1.kSchool     0000000000405004
&s2.kSchool     0000000000405004
&Student::kSchool       0000000000405004

&s1.kPi 0000000000405008
&s2.kPi 0000000000405008
&Student::kPi   0000000000405008


&s1.age_        0x61fe18
&s2.age_        0x61fe10

&s1.kGender     0x61fe1c
&s2.kGender     0x61fe14

&s1.kCount      0x408030
&s2.kCount      0x408030
&Student::kCount        0x408030

&s1.kSchool     0x405004
&s2.kSchool     0x405004
&Student::kSchool       0x405004

&s1.kPi 0x405008
&s2.kPi 0x405008
&Student::kPi   0x405008

请按任意键继续. . .
```

## 参考

[CSDN  | 不能在类内初始化非const static成员](https://blog.csdn.net/King_DJF/article/details/53582580?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-3)

[CSDN  | error: ‘constexpr’ needed for in-class initialization of static data member](https://blog.csdn.net/wphkadn/article/details/88174109)
