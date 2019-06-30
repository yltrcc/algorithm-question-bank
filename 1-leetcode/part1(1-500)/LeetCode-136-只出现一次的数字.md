# 描述

```text
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？
```

# 示例

```text
示例一：
    输入: [2,2,1]
    输出: 1
示例二：
    输入: [4,1,2,1,2]
    输出: 4
```

# 题目分析

```text
方法一：
    * 遍历数组，同时建立哈希表来记录每个数字在数组中出现的次数
    * 遍历哈希表找到只出现一次的数字

方法二：异或（XOR）运算
    * 两个相同的数 进行 异或 返回的结果是 0
    * 0 和 任意一个数 进行 异或 返回的结果是 这个数本身
所以对于本题，我们只需要将每个数进行异或最后剩下的数，就一定是只出现一次的那个数。

```

# 代码实现1

```text
class Solution {
    public int singleNumber(int[] nums) {
        HashMap<Integer, Integer> maps = new HashMap<>();

        int flag = -1;
        for (int i=0; i<nums.length; i++) {
            if (null == maps.get(nums[i])) {
                maps.put(nums[i], 1);
            }else {
                Integer tmp = maps.get(nums[i]) +1;
                 maps.put(nums[i], tmp);
            }
        }
        for (Map.Entry<Integer, Integer> entry : maps.entrySet()) {
            if (entry.getValue() == 1) {
                flag = entry.getKey();
            }
        }
        return flag;
    }
}
```

### 代码实现二

```text
class Solution {
    public int singleNumber(int[] nums) {

        int result = nums[0];
        for(int i=1; i<nums.length; i++) {
            result ^= nums[i];
        }

        return result;
    }
}
```