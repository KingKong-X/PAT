### **1143** **Lowest Common Ancestor**

### 题目描述：

The lowest common ancestor (LCA) of two nodes U and V in a tree is the deepest node that has both U and V as descendants.

A binary search tree (BST) is recursively defined as a binary tree which has the following properties:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
- Both the left and right subtrees must also be binary search trees.

Given any two nodes in a BST, you are supposed to find their LCA.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers: M (≤ 1,000), the number of pairs of nodes to be tested; and N (≤ 10,000), the number of keys in the BST, respectively. In the second line, N distinct integers are given as the preorder traversal sequence of the BST. Then M lines follow, each contains a pair of integer keys U and V. All the keys are in the range of **int**.

### Output Specification:

For each given pair of U and V, print in a line `LCA of U and V is A.` if the LCA is found and `A` is the key. But if `A` is one of U and V, print `X is an ancestor of Y.` where `X` is `A` and `Y` is the other node. If U or V is not found in the BST, print in a line `ERROR: U is not found.` or `ERROR: V is not found.` or `ERROR: U and V are not found.`.

### Sample Input:

```in
6 8
6 3 1 2 5 4 8 7
2 5
8 7
1 9
12 -3
0 8
99 99
```

### Sample Output:

```out
LCA of 2 and 5 is 3.
8 is an ancestor of 7.
ERROR: 9 is not found.
ERROR: 12 and -3 are not found.
ERROR: 0 is not found.
ERROR: 99 and 99 are not found.
```

### 题目大意：

给出一颗二叉查找树的先序遍历，找出某两个结点的最近的公共祖先。

M组测试案例，N个结点，每组测试案例都会给出两个数a，b，找出a和b的最近公共祖先。其中，a有可能是b的祖先，b有可能是a的祖先。如果a和b其中一个不在这棵树中，则输出ERROR。

### 思路：

一开始是想根据先序遍历构造这颗二叉查找树，后来发现太复杂了。

因为这颗二叉查找树是先序遍历的，先序遍历是根节点->左子树->右子树，因此在前面的数如果比后面的数大，那么前面的数一定是这个数的祖先。因此每组测试案例可以遍历所有的数，如果某个数比测试案例的都要大，那么这个数就是它们的最近公共祖先。如果刚好这个数和测试案例中的数相等，那么测试案例中的数会有一个是另一个的最近公共祖先。

可以用map<int,flag>去存放二叉查找树中的数，如果存在则为true，不存在则为false。

### 代码实现：

```c++
#include<iostream>
#include<map>
#include<vector>
using namespace std;
int main()
{
    int m,n;
    cin>>m>>n;
    vector<int> vec;
    map<int,bool> flag;
    for(int i=0;i<n;i++)
    {
        int a;
        cin>>a;
        vec.push_back(a);
        flag[a]=true;
    }
    for(int i=1;i<=m;i++)
    {
        int u,v;
        cin>>u>>v;
        if(!flag[u]&&!flag[v])
        {
            cout<<"ERROR: "<<u<<" and "<<v<<" are not found."<<endl;
        }
        else if(!flag[u])
        {
            cout<<"ERROR: "<<u<<" is not found."<<endl;
        }
        else if(!flag[v])
        {
            cout<<"ERROR: "<<v<<" is not found."<<endl;
        }
        else
        {
            for(int j=0;j<vec.size();j++)
            {
                if((vec[j]>=u&&vec[j]<=v)||(vec[j]<=u&&vec[j]>=v))
                {
                    if(vec[j]==u)
                    {
                        cout<<u<<" is an ancestor of "<<v<<"."<<endl;
                    }
                    else if(vec[j]==v)
                    {
                        cout<<v<<" is an ancestor of "<<u<<"."<<endl;
                    }
                    else
                    {
                        cout<<"LCA of "<<u<<" and "<<v<<" is "<<vec[j]<<"."<<endl;
                    }
                    break;
                }
            }
        }
    }
    return 0;
}
```

