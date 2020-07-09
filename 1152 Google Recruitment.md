# **1152** **Google Recruitment**

### 题目描述：

In July 2004, Google posted on a giant billboard along Highway 101 in Silicon Valley (shown in the picture below) for recruitment. The content is super-simple, a URL consisting of the first 10-digit prime found in consecutive digits of the natural constant *e*. The person who could find this prime number could go to the next step in Google's hiring process by visiting this website.

![prime.jpg](https://images.ptausercontent.com/57148679-d574-4f49-b048-775c6c07791c.jpg)

The natural constant *e* is a well known transcendental number（超越数）. The first several digits are: *e* = 2.71828182845904523536028747135266249775724709369995957496696762772407663035354759457138217852516642**7427466391**932003059921... where the 10 digits in bold are the answer to Google's question.

Now you are asked to solve a more general problem: find the first K-digit prime in consecutive digits of any given L-digit number.

### 输入规格：

Each input file contains one test case. Each case first gives in a line two positive integers: L (≤ 1,000) and K (< 10), which are the numbers of digits of the given number and the prime to be found, respectively. Then the L-digit number N is given in the next line.

### 输出规格：

For each test case, print in a line the first K-digit prime in consecutive digits of N. If such a number does not exist, output `404` instead. Note: the leading zeroes must also be counted as part of the K digits. For example, to find the 4-digit prime in 200236, 0023 is a solution. However the first digit 2 must not be treated as a solution 0002 since the leading zeroes are not in the original number.

### 案例输入1：

```in
20 5
23654987725541023819
```

### 案例输出1：

```out
49877
```

### 案例输入2：

```in
10 3
2468024680
```

### 案例输出2：

```out
404
```

### 题目大意：

在L位数字中找出第一个长度为K的素数，如果找不到则输出404；如果找到的数字有前导零那么需要保留

### 思路：

写一个isPrime函数判断一个数是否是素数，然后从第一位遍历到最后一位，每次遍历都会取出k位数（包括当前数）看是否是素数

### 代码实现：

```c++
#include<iostream>
#include<cmath>
#include<string>
using namespace std;
bool isPrime(int a)
{
    if(a<2) return false;
    else
    {
        for(int i=2;i<=sqrt(a);i++)
        {
            if(a%i==0) return false;
        }
    }
    return true;
}
int main()
{
    int l,k;
    string s,result,resultk;
    cin>>l>>k>>s;
    int temp,ck,ci;
    bool flag=false;
    for(int i=0;i<s.length();i++)
    {
        temp=0;
        ck=k-1;
        ci=i;
        result=resultk;
        for(int j=1;j<=k;j++)
        {
            temp=(s[ci]-'0')*pow(10,ck)+temp;
            result=result+s[ci];
            ck--;
            ci++;
        }
        if(isPrime(temp))
        {
            flag=true;
            break;
        }
    }
    if(!flag)
    {
        cout<<404;
    }
    else
    {
        cout<<result;
    }
    return 0;
}
```

### 注意：

由于pow函数的返回类型是double，因此得用一个double类型去接收，否则会出现精度错误。但是只有Dev-Cpp会出现这个问题，Clion和Vs studio不会出现这个问题。原因可能是另外两个编译器做了优化



