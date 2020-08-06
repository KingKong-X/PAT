# **1110** **Complete Binary Tree**

Given a tree, you are supposed to tell if it is a complete binary tree.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤20) which is the total number of nodes in the tree -- and hence the nodes are numbered from 0 to *N*−1. Then *N* lines follow, each corresponds to a node, and gives the indices of the left and right children of the node. If the child does not exist, a `-` will be put at the position. Any pair of children are separated by a space.

### Output Specification:

For each case, print in one line `YES` and the index of the last node if the tree is a complete binary tree, or `NO` and the index of the root if not. There must be exactly one space separating the word and the number.

### Sample Input 1:

```in
9
7 8
- -
- -
- -
0 1
2 3
4 5
- -
- -
```

### Sample Output 1:

```out
YES 8
```

### Sample Input 2:

```in
8
- -
4 5
0 6
- -
2 3
- 7
- -
- -
```

### Sample Output 2:

```out
NO 1
```

### 题目大意：

给出N个结点，每个结点包含左孩子和右孩子的值（同时值也代表着下标）。如果这颗树是完全二叉树，那么就输出YES和最后一个结点的值（下标）；否则就输出NO和根结点的值（下标）

### 思路：

所有的非叶子节点的个数等于N，则是完全二叉树，否则就不是完全二叉树。用深度优先遍历的方法去判断非叶子节点的个数。atoi是将字符串转换为数字的函数。

### 代码实现：

```C++
#include <iostream>
#include <string>
#include <cstring>
#include <cstdio>
#include <string.h>
using namespace std;
int h[100]={0};
int root=0,maxn=-1,ans=0;
class node
{
public:
    int l,r;
}a[25];
void dfs(int root,int index)
{
    if(index>maxn)
    {
        maxn=index;
        ans=root;
    }
    if(a[root].l!=-1)
    {
        dfs(a[root].l,index*2);
    }
    if(a[root].r!=-1)
    {
        dfs(a[root].r,index*2+1);
    }
}
int main()
{
    int n;
    cin>>n;
    for(int i=0;i<n;i++)
    {
        string left,right;
        cin>>left>>right;
        if(left=="-")
        {
            a[i].l=-1;
        }
        else
        {
            a[i].l=stoi(left);
            h[stoi(left)]=1;
        }
        if(right=="-")
        {
            a[i].r=-1;
        }
        else
        {
            a[i].r=stoi(right);
            h[stoi(right)]=1;
        }
    }
    while(h[root]==1)
    {
        root++;
    }
    dfs(root,1);
    if(maxn==n)
    {
        cout<<"YES"<<" "<<ans<<endl;
    }
    else
    {
        cout<<"NO"<<" "<<root<<endl;
    }
    return 0;
}
```