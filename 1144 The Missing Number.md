### **1144** **The Missing Number**

Given N integers, you are supposed to find the smallest positive integer that is NOT in the given list.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (≤105). Then N integers are given in the next line, separated by spaces. All the numbers are in the range of **int**.

### Output Specification:

Print in a line the smallest positive integer that is missing from the input list.

### Sample Input:

```in
10
5 -25 9 6 1 3 4 2 5 17
```

### Sample Output:

```out
7
```

### 题目大意：

给出N个整数，找出里面不存在的最小正数。

### 思路：

水题，将出现过的正数存入到数组里，然后进行遍历，当a[i]=0时，说明这个数没有出现过，则输出i。

### 代码实现：

```c++
#include<iostream>
#include<algorithm>
using namespace std;
int a[100005];
int main()
{
    int n;
    cin>>n;
    for(int i=1;i<=n;i++)
    {
        int b;
        cin>>b;
        if(b>0&&b<100005)
        {
            a[b]++;
        }
    }
    for(int i=1;i<=100002;i++)
    {
        if(a[i]==0)
        {
            cout<<i;
            break;
        }
    }
    return 0;
}
```