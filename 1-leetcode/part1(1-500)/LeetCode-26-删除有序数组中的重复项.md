# 题目链接

[https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

# 题目描述

给你一个有序数组 nums ，请你 原地 删除重复出现的元素，使每个元素 只出现一次 ，返回删除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。



说明:

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以「引用」方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```text
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
 
```

# 题目示例

```text
示例 1：

输入：nums = [1,1,2]
输出：2, nums = [1,2]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。
不需要考虑数组中超出新长度后面的元素。


示例 2：

输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。
不需要考虑数组中超出新长度后面的元素。

```

# 提示

- `0 <= nums.length <= 3 * 104`

- `-104 <= nums[i] <= 104`

- `nums` 已按升序排列

# 分析

这道题序列已经排序，那么像删除重复的项，只需要比对 $a^i 和 a_{i-1}$相等说明重复，不相等说明不重复。

这样的话就可以使用一个技巧：双指针法

- 快指针 fast表示遍历的下标位置，判断该项目和它的前一项，满指针 slow表示下一个不同元素要填入的下标位置，初始时两个指针都指向1

- 使用快指针fast遍历所有元素，nums[fast] ≠ nums[fast-1] 说明是不重复的元素，那么就有 nums[slow] = nums[fast]; slow++;

# 题解

```Java
class Solution {
    public int removeDuplicates(int[] nums) {
        
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int n = nums.length;
        int fast = 1, slow = 1;
        while (fast < n) {
            if (nums[fast] != nums[fast - 1]) {
                nums[slow] = nums[fast];
                ++slow;
            }
            ++fast;
        }
        return slow;
    }
}
```