### 题目来源

[https://leetcode-cn.com/problems/minimum-path-sum/](https://leetcode-cn.com/problems/minimum-path-sum/)

### 题目描述

```text
给定一个包含非负整数的 m x n 网格 grid ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

说明：每次只能向下或者向右移动一步。
```

![](https://secure1.wostatic.cn/static/rgVb55PQcLKMcicmt1FPkq/image.png)

### 示例

```text
示例一：
输入：grid = [[1,3,1],[1,5,1],[4,2,1]]
输出：7
解释：因为路径 1→3→1→1→1 的总和最小。

示例二：
输入：grid = [[1,2,3],[4,5,6]]
输出：12


```

### 题解

#### 题解1: 动态规划算法

具体算法思想请看：动态规划算法

```Java
/**
*  步骤一：定义数组元素的含义
*    定义dp[i][j] 从左上角到右下角 i,j的最小路径和
*  步骤二：找出初始值并设置边界条件
*    dp[0][0] = grid[0][0], 分别处于首行和首列的位置均可以直接求出值
*    dp[i][0] = dp[i-1] + grid[i][0]; m>i>=1  dp[0][i] = dp[0][i-1] + grid[0][i]; n>i>=1
*  步骤三：找出数组元素之间的关系式
*    dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i][j]; m>i>=1, n>j>=1
**/
class Solution {
    public int minPathSum(int[][] grid) {
    
        int[][] dp = new int[210][210];
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        int m = grid.length, n = grid[0].length;
        //初始化初始位置
        dp[0][0] = grid[0][0];
        //初始化首行
        for(int i=1; i<m; i++) {
            dp[i][0] = dp[i-1][0] + grid[i][0];
        }
        //初始化首列
        for(int i=1; i<n; i++) {
            dp[0][i] = dp[0][i-1] + grid[0][i];
        }
        for(int i=1; i<m; i++) {
            for(int j=1; j<n; j++) {
                dp[i][j] = Math.min(dp[i][j-1],dp[i-1][j]) + grid[i][j];
            }
        }
        return dp[m-1][n-1];
    }
}
```

```Java
/**
*  优化：二维dp转一维dp
**/
class Solution {
    public int minPathSum(int[][] grid) {
        int[] dp = new int[210];
        int m = grid.length, n = grid[0].length;
        //初始化初始位置
        dp[0] = grid[0][0];
        //初始化首行
        for(int i=1; i<n; i++) {
            dp[i] = dp[i-1] + grid[0][i];
        }
        for(int i=1; i<m; i++) {
            dp[0] += grid[i][0];
            for(int j=1; j<n; j++) {
                dp[j] = Math.min(dp[j], dp[j-1]) + grid[i][j];
            }
        }
        return dp[n-1];
    }
}
```