### **1147** **Heaps** 

### 题目描述：

In computer science, a **heap** is a specialized tree-based data structure that satisfies the heap property: if P is a parent node of C, then the key (the value) of P is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the key of C. A common implementation of a heap is the binary heap, in which the tree is a complete binary tree. (Quoted from Wikipedia at https://en.wikipedia.org/wiki/Heap_(data_structure))

Your job is to tell if a given complete binary tree is a heap.

### 输入规格:

Each input file contains one test case. For each case, the first line gives two positive integers: M (≤ 100), the number of trees to be tested; and N (1 < N ≤ 1,000), the number of keys in each tree, respectively. Then M lines follow, each contains N distinct integer keys (all in the range of **int**), which gives the level order traversal sequence of a complete binary tree.

### 输出规格:

For each given tree, print in a line `Max Heap` if it is a max heap, or `Min Heap` for a min heap, or `Not Heap` if it is not a heap at all. Then in the next line print the tree's postorder traversal sequence. All the numbers are separated by a space, and there must no extra space at the beginning or the end of the line.

### 案例输入1:

```in
3 8
98 72 86 60 65 12 23 50
8 38 25 58 52 82 70 60
10 28 15 12 34 9 8 56
```

### 案例输出1:

```out
Max Heap
50 60 65 72 12 23 86 98
Min Heap
60 58 52 38 82 70 25 8
Not Heap
56 12 34 28 9 8 15 10
```

### 题目大意：

M是测试案例的组数，N是结点个数。给出完全二叉树的N个结点的层序遍历，判断这个完全二叉树是最大堆、最小堆还是不是堆，同时输出这个完全二叉树的后序遍历。

### 思路：

后序遍历的访问顺序是左子树->右子树->根节点。

用数组存储N个结点的层序遍历顺序。

设根节点的下标是index，则左结点的下标是index✖2，右结点的下标是index✖2+1。

当下标大于N时进行回溯。

### 代码实现：

```c++
#include<iostream>
using namespace std;
int a[1005],n,m;
void postOrder(int index)
{
    // 回溯
    if(index>m)
    {
        return;
    }
    // 遍历左子树
    postOrder(index*2);

    // 遍历右子树
    postOrder(index*2+1);
    if(index==1)
    {
        cout<<a[index];
    }
    else
    {
        cout<<a[index]<<" ";
    }
}
int main()
{
    cin>>n>>m;
    while(n--)
    {
        int minHeap=0,maxHeap=0;
        for(int i=1;i<=m;i++)
        {
            cin>>a[i];
        }
        for(int i=2;i<=m;i++)
        {
            if(a[i/2]>a[i])
            {
                maxHeap=1;
            }
            else if(a[i/2]<a[i])
            {
                minHeap=1;
            }
        }
        if(maxHeap==1&&minHeap==1)
        {
            cout<<"Not Heap"<<endl;
        }
        else if(maxHeap==1)
        {
            cout<<"Max Heap"<<endl;
        }
        else
        {
            cout<<"Min Heap"<<endl;
        }
        postOrder(1);
        cout<<endl;
    }
    return 0;
}
```

