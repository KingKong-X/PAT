# **1108** **Finding Average**

The basic task is simple: given *N* real numbers, you are supposed to calculate their average. But what makes it complicated is that some of the input numbers might not be legal. A **legal** input is a real number in [−1000,1000] and is accurate up to no more than 2 decimal places. When you calculate the average, those illegal numbers must not be counted in.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤100). Then *N* numbers are given in the next line, separated by one space.

### Output Specification:

For each illegal input number, print in a line `ERROR: X is not a legal number` where `X` is the input. Then finally print in a line the result: `The average of K numbers is Y` where `K` is the number of legal inputs and `Y` is their average, accurate to 2 decimal places. In case the average cannot be calculated, output `Undefined` instead of `Y`. In case `K` is only 1, output `The average of 1 number is Y` instead.

### Sample Input 1:

```in
7
5 -3.2 aaa 9999 2.3.4 7.123 2.35
```

### Sample Output 1:

```out
ERROR: aaa is not a legal number
ERROR: 9999 is not a legal number
ERROR: 2.3.4 is not a legal number
ERROR: 7.123 is not a legal number
The average of 3 numbers is 1.38
```

### Sample Input 2:

```in
2
aaa -9999
```

### Sample Output 2:

```out
ERROR: aaa is not a legal number
ERROR: -9999 is not a legal number
The average of 0 numbers is Undefined
```

### 题目大意：

累加合法的数字，然后计算平均数

### 思路：

这道题的难点在于要筛选出合法的数字，这里用到sscanf和sprintf两个方法。

**sscanf() – 从一个字符串中读进与指定格式相符的数据
sprintf() – 字符串格式化命令，主要功能是把格式化的数据写入某个字符串中**

sscanf是从左到右进行转换，sprintf是从右到左进行转换，前提是可以转换。比如a="aaa"，那么就无法转换为temp，因为double类型无法表示aaa，所以b也没有办法从temp中进行转换

### 代码实现：

```c++
#include <iostream>
#include <cstdio>
#include <cstring>
using namespace std;
int main()
{
    int n;
    cin>>n;
    char a[50],b[50];
    double temp=0,sum=0;
    int cnt=0;
    bool flag=true;
    for(int i=0;i<n;i++)
    {
        flag=true;
        scanf("%s",a);
        sscanf(a,"%lf",&temp);// 将字符串转换为double类型
        sprintf(b,"%.2f",temp);// 将double类型转换为字符串类型
        for(int j=0;j<strlen(a);j++)
        {
            if(a[j]!=b[j])
            {
                flag=false;
            }
        }
        if(!flag||temp<-1000||temp>1000)
        {
            printf("ERROR: %s is not a legal number\n",a);
        }
        else
        {
            sum+=temp;
            cnt++;
        }
    }
    if(cnt==0)
    {
        printf("The average of 0 numbers is Undefined\n");
    }
    else if(cnt==1)
    {
        printf("The average of %d number is %.2f\n",cnt,sum/cnt);
    }
    else
    {
        printf("The average of %d numbers is %.2f\n",cnt,sum/cnt);
    }
    return 0;
}
```

