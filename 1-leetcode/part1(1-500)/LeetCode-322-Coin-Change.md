# 题目链接

[https://leetcode-cn.com/problems/coin-change/](https://leetcode-cn.com/problems/coin-change/)

# 题目描述

```text
给你一个整数数组 coins ，表示不同面额的硬币；以及一个整数 amount ，表示总金额。

计算并返回可以凑成总金额所需的 最少的硬币个数 。如果没有任何一种硬币组合能组成总金额，返回 -1 。

你可以认为每种硬币的数量是无限的。
```

# 题目示例

```text
示例 1：

输入：coins = [1, 2, 5], amount = 11
输出：3 
解释：11 = 5 + 5 + 1
示例 2：

输入：coins = [2], amount = 3
输出：-1
示例 3：

输入：coins = [1], amount = 0
输出：0
示例 4：

输入：coins = [1], amount = 1
输出：1
示例 5：

输入：coins = [1], amount = 2
输出：2

```

# 题目提示

```text
1 <= coins.length <= 12
1 <= coins[i] <= 231 - 1
0 <= amount <= 104
```

# 题目分析

```text
将原问题拆分成⼦问题
  已知什么？显⽽易⻅，钞票的⾦额都只需要其本身1张即可
  如何在已知钞票的情况下构造出 ⾦额X需要的最少钞票组合
确认状态
  DP[0] - DP[amount] 表示构造⾦额amount需要的最⼩钞票数
  确认边界状态（初始条件）
    DP[coin] = 1 其他的都未知初始值设为 -1
    例如coins = [1, 2, 5], amount = 11 已知 dp[1]、dp[2]、dp[5] =1
    现在已知 DP[coin] 需要求出每⼀个DP[amount]
状态转移方程
  dp[i] = min(dp[i-1], dp[i-2], dp[i-5]) + 1

```

# 题目代码

```Java
public int coinChange(int[] coins, int amount) {
   int len = coins.length;
   if (len == 0 || amount<0)
   return -1;
   if (amount==0)
   return 0;
   int [] dp = new int[amount+1];
   for (int i = 0; i <= amount; i++){
   dp[i] = -1;
   }
   for (int i = 0; i< len;i++){
   if(coins[i] == amount)
   return 1;
   if(coins[i] < amount)
   dp[coins[i]] = 1;
   }
   // State Transfer Function
   for(int i = 1; i <= amount;i++){
   for (int j = 0; j < len; j++){
   if (i - coins[j] >= 0 && dp[i - coins[j]] != -1){
   if (dp[i] == -1 || dp[i] > dp[i - coins[j]] + 1){
   dp[i] = dp[i - coins[j]] + 1;
   }
   }
   }
   }
   return dp[amount];
 }
```