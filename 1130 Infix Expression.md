# **1130** **Infix Expression** 

Given a syntax tree (binary), you are supposed to output the corresponding infix expression, with parentheses reflecting the precedences of the operators.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (≤ 20) which is the total number of nodes in the syntax tree. Then N lines follow, each gives the information of a node (the *i*-th line corresponds to the *i*-th node) in the format:

```
data left_child right_child
```

where `data` is a string of no more than 10 characters, `left_child` and `right_child` are the indices of this node's left and right children, respectively. The nodes are indexed from 1 to N. The NULL link is represented by −1. The figures 1 and 2 correspond to the samples 1 and 2, respectively.

| ![infix1.JPG](https://images.ptausercontent.com/4d1c4a98-33cc-45ff-820f-c548845681ba.JPG) | ![infix2.JPG](https://images.ptausercontent.com/b5a3c36e-91ad-494a-8853-b46e1e8b60cc.JPG) |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|                           Figure 1                           |                           Figure 2                           |

### Output Specification:

For each case, print in a line the infix expression, with parentheses reflecting the precedences of the operators. Note that there must be no extra parentheses for the final expression, as is shown by the samples. There must be no space between any symbols.

### Sample Input 1:

```in
8
* 8 7
a -1 -1
* 4 1
+ 2 5
b -1 -1
d -1 -1
- -1 6
c -1 -1
```

### Sample Output 1:

```out
(a+b)*(c*(-d))
```

### Sample Input 2:

```in
8
2.35 -1 -1
* 6 1
- -1 4
% 7 8
+ 2 3
a -1 -1
str -1 -1
871 -1 -1
```

### Sample Output 2:

```out
(a*2.35)+(-(str%871))
```

### 题目大意：

给出一颗语法树，输出它的中缀表达式

### 思路：

语法树有三种情况：

1、只有右子树而没有左子树

2、有左子树和右子树

3、没有左子树和右子树

语法树不可能出现只有左子树而没有右子树的情况。假设

![image-20200810222029839](C:\Users\42303\AppData\Roaming\Typora\typora-user-images\image-20200810222029839.png)

d现在放在左边，那么前序遍历就会出现d- ，这个是不符合语法的，所以只有d放在右边，那么前序遍历就会出现-d，这样才符合前序遍历

所以可以用递归的方法将语法树的三种情况填写上去即可

同样也需要找出根节点

### 代码：

```c++
#include<iostream>
#include<string>
using namespace std;
class node
{
public:
    string data;
    int left,right;
}a[25];
int have[25]={0};
string dfs(int root)
{
    if(a[root].left==-1&&a[root].right==-1)
    {
        return a[root].data;
    }
    if(a[root].left==-1&&a[root].right!=-1)
    {
        return "("+a[root].data+dfs(a[root].right)+")";
    }
    if(a[root].left!=-1&&a[root].right!=-1)
    {
        return "("+dfs(a[root].left)+a[root].data+dfs(a[root].right)+")";
    }
}
int main()
{
    int n;
    cin>>n;
    for(int i=1;i<=n;i++)
    {
        cin>>a[i].data>>a[i].left>>a[i].right;
        if(a[i].left!=-1)
        {
            have[a[i].left]=1;
        }
        if(a[i].right!=-1)
        {
            have[a[i].right]=1;
        }
    }
    // 找根结点
    int root=1;
    while(have[root]==1)
    {
        root++;
    }
    string ans=dfs(root);
    if(ans[0]=='(')
    {
        ans=ans.substr(1,ans.size()-2);
    }
    cout<<ans;
    return 0;
}
```

### 总结：

这道题的解法秒在递归，对递归还是不太熟悉

