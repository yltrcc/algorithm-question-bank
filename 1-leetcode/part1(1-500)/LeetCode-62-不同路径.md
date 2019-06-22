### 题目来源



### 题目描述

```text
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？
```

![](https://secure1.wostatic.cn/static/iNkG7kfhVH7sXRzXWbaKqD/image.png)

### 示例

```text
示例一：
输入：m = 3, n = 7
输出：28

示例二：
输入：m = 3, n = 2
输出：3
解释：
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右
3. 向下 -> 向右 -> 向下

示例3：
输入：m = 7, n = 3
输出：28

示例4：
输入：m = 3, n = 3
输出：6

```

### 题解

#### 题解1: 动态规划算法

具体算法思想请看：动态规划算法

```Java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[200][200];
        //初始条件
        for (int i=0; i<=n; i++) {
            dp[1][i] = 1;
        }
        for (int i=0; i<=m; i++) {
            dp[i][1] = 1;
        }
        for (int i=2; i<=m; i++) {
            for (int j=2; j<=n; j++) {
                dp[i][j] = dp[i][j-1] + dp[i-1][j];
            }
        }
        return dp[m][n];
    }
}
```

```Java
/**
* 代码优化：二维dp转一维dp
**/
class Solution {
    public int uniquePaths(int m, int n) {
        int[] dp = new int[110];
        //初始条件
        for (int i=0; i<=n; i++) {
            dp[i] = 1;
        }
        for (int i=2; i<=m; i++) {
            dp[0] = 1;
            for (int j=2; j<=n; j++) {
                dp[j] += dp[j-1];
            }
        }
        
        return dp[n];
    }
}

```

#### 题解2:组合数学

具体算法思想请看：排列组合

```text
还在研究没搞懂
```