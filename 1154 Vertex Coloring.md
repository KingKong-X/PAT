# **1154** **Vertex Coloring**

### 题目描述：

A **proper vertex coloring** is a labeling of the graph's vertices with colors such that no two vertices sharing the same edge have the same color. A coloring using at most *k* colors is called a (proper) ***k\*-coloring**.

Now you are supposed to tell if a given coloring is a proper *k*-coloring.

### 输入规格：

Each input file contains one test case. For each case, the first line gives two positive integers *N* and *M* (both no more than 104), being the total numbers of vertices and edges, respectively. Then *M* lines follow, each describes an edge by giving the indices (from 0 to *N*−1) of the two ends of the edge.

After the graph, a positive integer *K* (≤ 100) is given, which is the number of colorings you are supposed to check. Then *K* lines follow, each contains *N* colors which are represented by non-negative integers in the range of **int**. The *i*-th color is the color of the *i*-th vertex.

### 输出规格：

For each coloring, print in a line `k-coloring` if it is a proper `k`-coloring for some positive `k`, or `No` if not.

### 案例输入1：

```in
10 11
8 7
6 8
4 5
8 4
8 1
1 2
1 4
9 8
9 1
1 0
2 4
4
0 1 0 1 4 1 0 1 3 0
0 1 0 1 4 1 0 1 0 0
8 1 0 1 4 1 0 5 3 0
1 2 3 4 5 6 7 8 8 9
```

### 案例输出1：

```out
4-coloring
No
6-coloring
No
```

### 题目大意：

有n个顶点，m条边，每个顶点都有一种颜色，看有边相领的两个顶点是否是同一种颜色。如果是同一种颜色，输出No；否则输出n个顶点中一共有多少种颜色。

### 代码实现：

```c++
#include<iostream>
#include<vector>
#include<set>
using namespace std;
class node
{
public:
    int start;//起点编号
    int end;//终点编号
};
int main()
{
    int n,m;
    cin>>n>>m;
    //用vector存储m条边的信息
    vector<node> vertex(m);
    for(int i=0;i<m;i++)
    {
        cin>>vertex[i].start>>vertex[i].end;
    }
    int k;
    cin>>k;
    int a[100009];
    bool flag;
    for(int i=1;i<=k;i++)
    {
        flag=true;
        //set有自动去重的作用
        set<int> s;
        //输入每个顶点的颜色
        for(int j=0;j<n;j++)
        {
            cin>>a[j];
            s.insert(a[j]);
        }
        //看有边相领的两个顶点的颜色是否一样
        for(int j=0;j<m;j++)
        {
            if(a[vertex[j].start]==a[vertex[j].end])
            {
                flag=false;
                break;
            }
        }
        if(flag)
        {
            cout<<s.size()<<"-coloring"<<endl;
        }
        else
        {
            cout<<"No"<<endl;
        }
    }
    return 0;
}
```

### 注意：

set是一个内部自动有序且不含重复元素的容器

上述代码需注意vector<node> vertex(m)和vector<node> vertex[m]的区别。前者代表长度为m的一维数组，后者代表一维是m，二维长度可变的二维数组

