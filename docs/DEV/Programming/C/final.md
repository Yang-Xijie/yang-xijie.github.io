# C 语言期末考试常用函数

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
/*选择排序——元素p[a]~p[b]升序排序*/
void selesort(int p[], int a, int b);
/*冒泡排序——整体升序排序*/
void bubsort(int p[], int n);
/*求余矩阵——输入矩阵A，求删掉第0列第i行的矩阵B，其中B是一个空的地址，用来存放矩阵元素*/
void smallermatrix(int a[], int b[], int n, int i);
/*求n阶方阵A行列式——A以一维数组形式输入*/
int det(int a[], int n);
/* 判断素数——输入一个正整数n,是素数返回1，不是返回0 */
int sushu(int n);
/* 矩阵相乘——输入一维数组A m*n, B n*p, 空的已经申请好的数组C m*p，将A*B放在C中 */
void matrixmul(int a[], int b[], int c[], int m, int n, int p);
/* 矩阵转置——输入一维数组A m*n,空的已经申请好的数组C n*m，将A转置放在C中 */
void matrixtran(int a[], int c[], int m, int n);


/*选择排序——元素p[a]~p[b]升序排序*/
void selesort(int p[], int a, int b)
{
    int i, j, k;
    int d;                       //用来交换的变量
    for (i = a; i <= b - 1; i++) //对最后一个元素p[n-1]不用操作
    {
        k = i; //记录现在到哪里了
        for (j = i + 1; j <= b; j++)
            if (p[j] < p[k])
                k = j; //从i的下一个开始找，如果有比i小元素（第j个）的就让k为j
                       //本质目的是找出i后面最小的一个
        if (k != i)    //如果i项不是最小的，那么换！
        {
            d = p[i];
            p[i] = p[k];
            p[k] = d;
        }
    }
}
/*冒泡排序——整体升序排序*/
void bubsort(int p[], int n)
{
    int m, k; //m记录最右边的项，k记录最左边的项
    int j, i;
    int d; //用来交换元素
    k = 0;
    m = n - 1;
    while (k < m)
    {
        j = m - 1;
        m = 0;
        for (i = k; i <= j; i++) //让最大的跑到右边去
            if (p[i] > p[i + 1])
            {
                d = p[i];
                p[i] = p[i + 1];
                p[i + 1] = d;
                m = i; //相当于m在原来的基础上减一
            }
        /*倒着再排*/
        j = k + 1;
        k = 0;
        for (i = m; i >= j; i--) //让最小的跑到左边去
            if (p[i - 1] > p[i])
            {
                d = p[i];
                p[i] = p[i - 1];
                p[i - 1] = d;
                k = i; //相当于k在原来的基础上加一
            }
    }
}
/*求余矩阵——输入矩阵A，求删掉第0列第i行的矩阵B，其中B是一个空的地址，用来存放矩阵元素*/
void smallermatrix(int a[], int b[], int n, int i)
{
    int p, q; //p是A的行数，q是B的列数
    for (p = 0; p <= n - 1; p++)
    {
        if (p < i) //在第i行之前，直接赋值
            for (q = 0; q <= n - 2; q++)
                b[p * (n - 1) + q] = a[p * n + q + 1];
        if (p > i) //在第i行之后，b那里不能往下跳，减个1就行了
            for (q = 0; q <= n - 2; q++)
                b[(p - 1) * (n - 1) + q] = a[p * n + q + 1];
    }
}
/*求n阶方阵A行列式——A以一维数组形式输入*/
int det(int a[], int n) //需要使用上面的smallermatrix函数
{
    int i = 0, j = 0;
    int sum = 0;
    int *b;
    int flag = 1;
    if (n == 2)
        return ((a[0] * a[3]) - (a[1] * a[2])); //针对二阶行列式直接上公式
    else
    {
        for (sum = 0, flag = 1, i = 0; i <= n - 1; i++)
        {
            b = (int *)malloc((n - 1) * (n - 1) * sizeof(int)); //申请B的内存
            smallermatrix(a, b, n, i);                          //求删掉A第0列第i行元素的矩阵，给B
            sum += flag * (a[i * n] * det(b, n - 1));           //累加
            flag *= -1;                                         //每往下一行都要变号，相当于-1的某次方
            free(b);
        }
        return sum;
    }
}
/* 判断素数——输入一个正整数n，是素数返回1，不是返回0 */
int sushu(int n)
{

    int i, flag;
    if (n == 1)
        return 0;
    if (n == 2)
        return 1;
    for (i = 2, flag = 1; i <= sqrt(n) && flag == 1; i++)
    {
        if (n % i == 0)
            flag = 0; //有一个能整除n，n就不是素数了
    }
    return flag;
}
/* 矩阵相乘——输入一维数组A m*n, B n*p, 空的已经申请好的数组C m*p，将A*B放在C中 */
void matrixmul(int a[], int b[], int c[], int m, int n, int p)
{
    int i, j, k, sum;
    for (i = 0; i <= m - 1; i++)
    {
        for (j = 0, sum = 0; j <= p - 1; j++)
        {
            for (sum = 0, k = 0; k <= n - 1; k++)
            {
                sum += a[i * n + k] * b[k * p + j];
            }
            c[i * p + j] = sum;
        }
    }
}
/* 矩阵转置——输入一维数组A m*n,空的已经申请好的数组C n*m，将A转置放在C中 */
void matrixtran(int a[], int c[], int m, int n)
{
    int i, j;
    for (i = 0; i <= n - 1; i++)
    {
        for (j = 0; j <= m - 1; j++)
        {
            c[i * m + j] = a[j * n + i];
        }
    }
}
/* 大型整数相乘 */
int main()
{
    char num1[1000], num2[1000];
    int a[2000] = {0};
    int n, i, j, k, l1, l2;
    printf("please input two integers:\n");
    scanf("%s%s", num1, num2);
    printf("%s*%s=", num1, num2); //为了之后的输出
    l1 = strlen(num1);
    l2 = strlen(num2);
    /* 将字符转化为数字 */
    for (n = 0; n < l1; n++)
        num1[n] -= '0';
    for (n = 0; n < l2; n++)
        num2[n] -= '0';
    /* 第l1-1位*第l2-1位放在第0位(乘积最小的一位),第0位*第0位放在第l1-1+l2-1位(乘积最大的一位) */
    for (i = 0; i <= l1 - 1; i++)
        for (j = 0; j <= l2 - 1; j++)
            a[l1 - 1 - i + l2 - 1 - j] += num1[i] * num2[j];
    /* 从最小的一位开始——低位置为单位数，并将十位进到高位 */
    for (n = 0; n <= l1 + l2; n++)
    {
        a[n + 1] += a[n] / 10;
        a[n] %= 10;
    }
    /* 从最后往前找第一个非零位 */
    for (n = l1 + l2 + 1; a[n] == 0; n--)
        k = n;
    /* 从非零位的前一位开始打印 */
    for (n = k - 1; n >= 0; n--)
        printf("%d", a[n]);
    printf("\n");
    system("pause");
}
```
