# 题目链接

[https://leetcode-cn.com/problems/maximal-square/](https://leetcode-cn.com/problems/maximal-square/)

# 题目描述

```Java
在一个由 '0' 和 '1' 组成的二维矩阵内，找到只包含 '1' 的最大正方形，并返回其面积。

```

# 题目示例

```text
示例1：

输入：matrix = [
  ["1","0","1","0","0"],
  ["1","0",**"1","1","1"**],
  ["1","1",**"1","1","1"**],
  ["1","0","0","1","0"]]
  注意加粗部分，是个2 * 3 的长方形，可以看做两个 2 * 2 的正方形重合而成，所以最大正方形是2 * 2 = 4
输出：4

示例2：

输入：matrix = [
  ["0","1"],
  ["1","0"]]
输出：1

示例 3：

输入：matrix = [["0"]]
输出：0

```

# 题目分析

```text
1、⾸先我们定义 dp[i][j] 含义为正⽅形以 dp[i][j] 作为右下⻆时的最⼤边⻓值。
2、接着我们来推导他们的关系
  显然，对于任意⼀点 dp[i][j]，由于该点是正⽅形的右下⻆，
  所以该点的右边，下边，右下边都不⽤考虑，关⼼的是左边，上边，和左上边，也就是我们要推导 
  dp[i][j] 与 dp[i-1][j]、dp[i][j-1]、dp[i-1][j-1]之间的关系。
  
  他们有如下关系
    dp[i][j] = min( dp[i-1][j], dp[i-1][j-1], dp[i][j-1] ）+ 1
这个关系其实也不算难推，毕竟不能有 0 存在，所以只能取交他们三个点的交集。你们可以画个图，可能就⽐较好理解了。

```

# 题目代码

## 题解一：暴力法

```text
public int maximalSquare(char[][] matrix) {
   // 如果矩阵⻓或宽少于1则直接返回0
   if(matrix.length < 1 || matrix[0].length < 1)
   return 0;
   
   int rows = matrix.length;
   int cols = matrix[0].length;
   // 记录最⼤边⻓
   int max = 0;
   for (int i = 0; i < rows; i++) {
   for (int j = 0; j < cols; j++) {
   // 把（i，j）作为左上⻆向右下⻆搜索
   if (matrix[i][j] == '1') {
   // 此时正⽅形的边⻓
   int sqlen = 1;
   boolean flag = true;//记录是否遇到0的位置
   while (sqlen + i < rows && sqlen + j < cols && flag) {
   for (int k = j; k <= sqlen + j; k++) {
   if (matrix[i + sqlen][k] == '0') {
   flag = false;
   break;
   }
   }
   for (int k = i; k <= sqlen + i; k++) {
   if (matrix[k][j + sqlen] == '0') {
   flag = false;
   break;
   }
   }
   if (flag)
   sqlen++;
   }
   if (max < sqlen) {
   max = sqlen;
   }
   }
   }
   }
   return max * max;
}
```

## 题解二：动态规划

```text
public int maximalSquare(char[][] matrix) {
   // 如果矩阵⻓或宽少于1则直接返回0
   if(matrix.length < 1 || matrix[0].length < 1)
   return 0;
   int rows = matrix.length;
   int cols = matrix[0].length;
   
   int[][] dp = new int[rows + 1][cols + 1];
   int max = 0;
   for (int i = 1; i <= rows; i++) {
   for (int j = 1; j <= cols; j++) {
   if (matrix[i-1][j-1] == '1'){
   dp[i][j] = Math.min(Math.min(dp[i][j - 1], dp[i - 1][j]),
  dp[i - 1][j - 1]) + 1;
   max = Math.max(max, dp[i][j]);
   }
   }
   }
   return max * max;
}
```

## 题解三：动态规划优化

```text
# dp[i][j] = min( dp[i-1][j], dp[i-1][j-1], dp[i][j-1] ）+ 1

public int maximalSquare(char[][] matrix) {
   if(matrix.length < 1 || matrix[0].length < 1)
   return 0;
   int rows = matrix.length;
   int cols = matrix[0].length;
   int[] dp = new int[cols + 1];
   int max = 0, prev = 0;
   for (int i = 1; i <= rows; i++) {
   for (int j = 1; j <= cols; j++) {
   int temp = dp[j];
   if (matrix[i - 1][j - 1] == '1') {
   dp[j] = Math.min(Math.min(dp[j - 1], prev), dp[j]) + 1;
   max = Math.max(max, dp[j]);
   } else {
   dp[j] = 0;
   }
   prev = temp;
   }
   }
   return max * max;
}

```