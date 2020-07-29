### **1140** **Look-and-say Sequence** 

Look-and-say sequence is a sequence of integers as the following:

```
D, D1, D111, D113, D11231, D112213111, ...
```

where `D` is in [0, 9] except 1. The (n+1)st number is a kind of description of the nth number. For example, the 2nd number means that there is one `D` in the 1st number, and hence it is `D1`; the 2nd number consists of one `D` (corresponding to `D1`) and one 1 (corresponding to 11), therefore the 3rd number is `D111`; or since the 4th number is `D113`, it consists of one `D`, two 1's, and one 3, so the next number must be `D11231`. This definition works for `D` = 1 as well. Now you are supposed to calculate the Nth number in a look-and-say sequence of a given digit `D`.

### Input Specification:

Each input file contains one test case, which gives `D` (in [0, 9]) and a positive integer N (≤ 40), separated by a space.

### Output Specification:

Print in a line the Nth number in a look-and-say sequence of `D`.

### Sample Input:

```in
1 8
```

### Sample Output:

```out
1123123111
```

### 题目大意：

给出第一个数字D，输出进行N次变换后的字符串。

如：

１：１

２：１１（１个１）

３：１２（２个１）

４：１１２１（１个１，１个２）

５：１２２１１１（２个１，１个２，１个１）

６：１１２２１３（１个１，２个２，３个１）

７：１２２２１１３１（２个１，２个２，１个１，１个３）

８：１１２３１２３１１１（１个１，３个２，２个１，１个３，１个１）

注：数字写在前面，数字的个数写在后面

### 思路：

首先需要写个函数将数字出现的个数转化为字符串

然后进行双重循环, 外层循环进行N-1次, 因为第一次就是输入中的D, 内层循环是遍历第i次变换后的字符串, 如果是ans[j]和ans[j+1]相等, 那么次数＋1, 同时j++, 最后再append进newAns, 再将newAns赋值给ans

### 代码实现:

```c++
#include<iostream>
#include<string>
#include<algorithm>
using namespace std;
// 次数转字符串
string get(int a)
{
    string ans;
    while(a!=0)
    {
        // 如果是ans=ans+(a%10+'0')就会报错，同时花费的时间也会增多
        ans+=(a%10+'0');
        a=a/10;
    }
    reverse(ans.begin(),ans.end());
    return ans;
}
int main()
{
    string a;
    int b;
    cin>>a>>b;
    string ans=a;
    string newAns;
    for(int i=1;i<b;i++)
    {
        for(int j=0;j<ans.length();j++)
        {
            int cnt=1;
            while(j<ans.length()-1&&ans[j]==ans[j+1])
            {
                cnt++;
                j++;
            }
            // append的速度比+要快得多
            newAns.append(ans[j]+get(cnt));
        }
        ans=newAns;
        newAns="";
    }
    cout<<ans;
    return 0;
}
```

### 总结:

字符串中的append函数要比直接+快, 同时+=比+快