# **1155** **Heap Paths**

### 题目描述：

In computer science, a **heap** is a specialized tree-based data structure that satisfies the heap property: if P is a parent node of C, then the key (the value) of P is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the key of C. A common implementation of a heap is the binary heap, in which the tree is a complete binary tree. (Quoted from Wikipedia at https://en.wikipedia.org/wiki/Heap_(data_structure))

One thing for sure is that all the keys along any path from the root to a leaf in a max/min heap must be in non-increasing/non-decreasing order.

Your job is to check every path in a given complete binary tree, in order to tell if it is a heap or not.

### 输入规格：

Each input file contains one test case. For each case, the first line gives a positive integer *N* (1<*N*≤1,000), the number of keys in the tree. Then the next line contains *N* distinct integer keys (all in the range of **int**), which gives the level order traversal sequence of a complete binary tree.

### 输出规格：

For each given tree, first print all the paths from the root to the leaves. Each path occupies a line, with all the numbers separated by a space, and no extra space at the beginning or the end of the line. The paths must be printed in the following order: for each node in the tree, all the paths in its right subtree must be printed before those in its left subtree.

Finally print in a line `Max Heap` if it is a max heap, or `Min Heap` for a min heap, or `Not Heap` if it is not a heap at all.

### 案例输入1：

```in
8
98 72 86 60 65 12 23 50
```

### 案例输出1：

```out
98 86 23
98 86 12
98 72 65
98 72 60 50
Max Heap
```

### 案例输入2：

```in
8
8 38 25 58 52 82 70 60
```

### 案例输出2：

```out
8 25 70
8 25 82
8 38 52
8 38 58 60
Min Heap
```

### 案例输入3：

```in
8
10 28 15 12 34 9 8 56
```

### 案例输出3：

```out
10 15 8
10 15 9
10 28 34
10 28 12 56
Not Heap
```

### 题目大意：

首先输入一个正整数n，然后输入n个正整数，判断是最大堆（父结点比左子树和右子树都大）、最小堆（父结点比左子树和右子树都小）或者不是堆中的哪一种。同时输出这个二叉树的每一条路径（先输出右子树的路径，再输出左子树的路径）

### 思路：

在二叉树中，设根节点下标为index，那么左结点的下标index✖2，右结点的下标为index✖2+1。

所以可以递归地输出二叉树的路径。

用vector来储存、删除二叉树中的结点，用数组存储所有结点。

### 代码实现：

``

```c++
#include<iostream>
#include<vector>
using namespace std;
int n;
int a[1005];
vector<int> v;
void dfs(int index)
{
    if(index*2>n&&index*2+1>n)
    {
        if(index<=n)
        {
            for(int i=0;i<v.size();i++)
            {
                if(i==0)
                {
                    cout<<v[i];
                }
                else
                {
                    cout<<" "<<v[i];
                }
            }
            cout<<endl;
        }
    }
    else
    {
        // 不断地去搜索右子树
        v.push_back(a[index*2+1]);
        dfs(index*2+1);

        // 回溯时，将右子树删除
        v.pop_back();

        // 不断地去搜索左子树
        v.push_back(a[index*2]);
        dfs(index*2);

        // 回溯时，将左子树删除
        v.pop_back();
    }
}
int main()
{
    cin>>n;
    for(int i=1;i<=n;i++)
    {
        cin>>a[i];
    }
    v.push_back(a[1]);
    dfs(1);
    int b=1,c=1;
    for(int i=2;i<=n;i++)
    {
        if(a[i/2]<a[i])
        {
            b=0;
        }
        if(a[i/2]>a[i])
        {
            c=0;
        }
    }
    if(b==0&&c==0)
    {
        cout<<"Not Heap"<<endl;
    }
    else if(c==0)
    {
        cout<<"Max Heap"<<endl;
    }
    else if(b==0)
    {
        cout<<"Min Heap"<<endl;
    }
    return 0;
}
```

### 总结：

看到这个题目时，首先想到的是用链表去把二叉树构建起来，但是却非常繁琐。后来想到可以用数组的方法去构建，然后利用二叉树的性质去找左子树和右子树，接着再递归存入vector中即可。