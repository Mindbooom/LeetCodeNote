## Tag:
Medium;dp;
## Description :
把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率。  

你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。
```c++
示例 1:

输入: 1
输出: [0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]
示例 2:

输入: 2
输出: [0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13

```
## Solution:
```c++
/*
确定问题解的表达式。可将f(n, s) 表示n个骰子点数的和为s的排列情况总数
确定状态转移方程。n个骰子点数和为s的种类数只与n-1个骰子的和有关。因为一个骰子有六个点数，那么第n个骰子可能出现1到6的点数。所以第n个骰子点数为1的话，f(n,s)=f(n-1,s-1)，当第n个骰子点数为2的话，f(n,s)=f(n-1,s-2)，…，依次类推。在n-1个骰子的基础上，再增加一个骰子出现点数和为s的结果只有这6种情况！那么有：f(n,s)=f(n-1,s-1)+f(n-1,s-2)+f(n-1,s-3)+f(n-1,s-4)+f(n-1,s-5)+f(n-1,s-6)
上面就是状态转移方程，已知初始阶段的解为：当n=1时, f(1,1)=f(1,2)=f(1,3)=f(1,4)=f(1,5)=f(1,6)=1。
*/

class Solution {
public:
    vector<double> twoSum(int n) {
        vector<vector<int>>dp(n+1,vector<int>(6*n+1,0));
        double num = pow(6,n);
        vector<double>res(5*n+1,1/(double)6);
        for(int i =1;i<=6;i++)
        dp[1][i]=1;//只有一个骰子的时候，每种情况出现的次数均为1
        for(int i = 2;i<=n;i++)
        {
            for(int j = i;j<=6*n; j++)
            {
                for(int k =1;k<=6;k++)
                {
                    if(j-k>0)dp[i][j] += dp[i-1][j-k]; 
                    if(i==n)res[j-i]=dp[i][j]/num;
                }
            }

        }
        return res;
    }
};
```

## Thought:
[leetcode](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/comments/)

