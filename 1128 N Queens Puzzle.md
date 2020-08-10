# **1128** **N Queens Puzzle**

The "eight queens puzzle" is the problem of placing eight chess queens on an 8×8 chessboard so that no two queens threaten each other. Thus, a solution requires that no two queens share the same row, column, or diagonal. The eight queens puzzle is an example of the more general *N* queens problem of placing *N* non-attacking queens on an *N*×*N* chessboard. (From Wikipedia - "Eight queens puzzle".)

Here you are NOT asked to solve the puzzles. Instead, you are supposed to judge whether or not a given configuration of the chessboard is a solution. To simplify the representation of a chessboard, let us assume that no two queens will be placed in the same column. Then a configuration can be represented by a simple integer sequence (*Q*1,*Q*2,⋯,*Q**N*), where *Q**i* is the row number of the queen in the *i*-th column. For example, Figure 1 can be represented by (4, 6, 8, 2, 7, 1, 3, 5) and it is indeed a solution to the 8 queens puzzle; while Figure 2 can be represented by (4, 6, 7, 2, 8, 1, 9, 5, 3) and is NOT a 9 queens' solution.

| ![8q.jpg](https://images.ptausercontent.com/7d0443cf-5c19-4494-98a6-0f0f54894eaa.jpg) |      | ![9q.jpg](https://images.ptausercontent.com/d187e37a-4eb8-4215-8e2c-040a73c5c8d8.jpg) |
| :----------------------------------------------------------: | ---- | :----------------------------------------------------------: |
|                           Figure 1                           |      |                           Figure 2                           |

### Input Specification:

Each input file contains several test cases. The first line gives an integer *K* (1<*K*≤200). Then *K* lines follow, each gives a configuration in the format "*N* *Q*1 *Q*2 ... *Q**N*", where 4≤*N*≤1000 and it is guaranteed that 1≤*Q**i*≤*N* for all *i*=1,⋯,*N*. The numbers are separated by spaces.

### Output Specification:

For each configuration, if it is a solution to the *N* queens problem, print `YES` in a line; or `NO` if not.

### Sample Input:

```in
4
8 4 6 8 2 7 1 3 5
9 4 6 7 2 8 1 9 5 3
6 1 5 2 6 4 3
5 1 3 5 2 4
```

### Sample Output:

```out
YES
NO
NO
YES
```

### 题目大意：

给出N组测试案例，每组给出K个数字，判断这K个数字是否可以构成N皇后的一个解决方案

### 思路：

水题一道

由于确定了每一列都不会出现两个皇后，因此只需要考虑行和对角线是否有皇后

判断对角线有个公式是：abs(a[i]-a[j])==abs(i-j)

### 代码实现：

```c++
#include<iostream>
#include<vector>
#include<cmath>
using namespace std;
int main()
{
    int k;
    cin>>k;
    while(k--)
    {
        int n;
        cin>>n;
        vector<int> v;
        for(int i=0;i<n;i++)
        {
            int a;
            cin>>a;
            v.push_back(a);
        }
        bool flag=true;
        for(int i=0;i<n;i++)
        {
            for(int j=i+1;j<n;j++)
            {
                if(v[i]==v[j]||abs(v[i]-v[j])==abs(i-j))
                {
                    flag=false;
                    break;
                }
            }
            if(!flag)
            {
                break;
            }
        }
        if(!flag)
        {
            cout<<"NO"<<endl;
        }
        else
        {
            cout<<"YES"<<endl;
        }
    }
    return 0;
}
```