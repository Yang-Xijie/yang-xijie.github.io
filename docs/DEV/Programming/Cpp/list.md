# C++ 笔记 ｜ 类的应用实例：单链表封装

## 用两个类表达一个概念

* 链表结点（ListNode）类
* 链表（List）类

```cpp
//listnode.h
#ifndef LISTNODE_H
#define LISTNODE_H

class List;    // 链表类定义（复合方式）
class ListNode // 链表结点类
{
public:
    friend class List;              // 链表类为其友元类
    ListNode(int x, ListNode *next) //构造函数
    {
        this->data = x;
        this->next = next;
    }

private:
    int data;       //结点数据, 整型
    ListNode *next; //结点指针
};

class List //链表类
{
public:
    List() { first = current = NULL; } //构造函数,使新建的链表成为空链表
    int insertData(int x, int i);
    int removeData(int &x, int i);
    void displayAll();

private:
    ListNode *first, *current; //表头指针，当前指针
};

#endif // LISTNODE_H
```

```cpp
//listnode.cpp
#include <iostream>
using namespace std;

#include"listnode.h"

//在链表第i个结点处插入新元素x,成功返回1,失败返回0
int List ::insertData(int x, int i) 
{
    ListNode *p = current;
    current = first;
    for (int k = 0; k < i - 1; k++) //找第 i-1个结点
    {
        if (current == NULL)
            break;
        else
            current = current->next;
    }
    if (current == NULL && first != NULL)
    {
        cout << "无效的插入位置!\n";
        current = p;
        return 0;
    }
    ListNode *newnode = new ListNode(x, NULL);
    if (first == NULL || i == 0) //插在表前
    {
        newnode->next = first;
        first = current = newnode;
    }
    else //插在表中间或表尾
    {
        newnode->next = current->next;
        current = current->next = newnode;
    }
    return 1;
}

//在链表中删除第i个结点,通过x返回其值
int List ::removeData(int &x, int i)
{
    ListNode *p, *q;
    if (i == 0) //删除表中第 1 个结点
    {
        q = first;
        current = first = first->next;
    }
    else
    {
        p = current;
        current = first;
        //找第 i-1个结点
        for (int k = 0; k < i - 1; k++)
        {
            if (current == NULL)
                break;
            else
                current = current->next;
        }
        if (current == NULL || current->next == NULL)
        {
            cout << "无效的删除位置!\n";
            current = p;
            return 0;
        }
        else //删除表中间或表尾元素
        {
            q = current->next; //重新链接
            current = current->next = q->next;
        }
    }
    x = q->data; // 返回第 i 个结点的值
    delete q;    // 删除链表节点q
    return 1;
}

//显示链表中所有数据
void List ::displayAll()
{
    ListNode *p = first;
    while (p)
    {
        cout << p->data << ',';
        p = p->next;
    }
    cout << endl;
}
```

```cpp
//main.cpp
#include <stdlib.h>
#include <iostream>
#include "listnode.h"
using namespace std;

int main()
{
    List A;//新建空链表A
    int x, i;
    for (i = 0; i < 10; i++)
        A.insertData(i, 0); // 每个元素插在链表头部(在链表0的地方插入元素i)
    A.displayAll();
    for (i = 0; i < 10; i++)
    {
        if (A.removeData(x, 0)) // 删除链表第一个元素
            cout << x << ',';
    }
    A.displayAll();
    cout << endl;
    
    system("pause");
}
```

```cpp
//结果
9,8,7,6,5,4,3,2,1,0,
9,8,7,6,5,4,3,2,1,0,

Press any key to continue . . .
```
