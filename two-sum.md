# Two Sum

### 题目

> Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.
>
> You may assume that each input would have **exactly** one solution, and you may not use the same element twice.

### 翻译

> 给定一组整数，将两个数的返回指数相加，使它们相加成一个特定的目标。
>
> 您可以假设每个输入都有一个解决方案，您可能不会使用相同的元素两次。

### 例子

> Given nums = \[2, 7, 11, 15\], target = 9,
>
> Because nums\[0\] + nums\[1\] = 2 + 7 = 9,
>
> return \[0, 1\].

---

Runtime: **3** **ms**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] map = new int[20050];
        int size = 4;
        for (int i = 0; i < nums.length; i++) {
            map[nums[i] + size] = (i + 1);
            int diff = target - nums[i + 1] + size;
            if (diff < 0) continue;
            int d = map[diff];
            if (d > 0)
                return new int[]{d - 1, i + 1};
        }
        return null;
    }
}
```

Runtime: **4** **ms**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        int numMin = Integer.MAX_VALUE;
        int numMax = Integer.MIN_VALUE;

        for (int num : nums) {
            if (num < numMin) {
                numMin = num;
            }

            if (num > numMax) {
                numMax = num;
            }
        }

        int max = target - numMin;
        int min = target - numMax;

        int targetMax = max > numMax ? numMax : max;
        int targetMin = min < numMin ? numMin : min;

        int[] numIndices = new int[targetMax - targetMin + 1];

        for (int i = 0; i <= numIndices.length - 1; i++) {
            numIndices[i] = -1;
        }

        for (int i = 0; i <= nums.length - 1; i++) {
            if (nums[i] >= targetMin && nums[i] <= targetMax) {
                int offset = -targetMin;
                if (numIndices[(target - nums[i]) + offset] != -1) {
                    return new int[]{numIndices[(target - nums[i]) + offset], i};
                } else {
                    numIndices[nums[i] + offset] = i;
                }
            }
        }
        return new int[]{0, 0};
    }
}
```

---

### 第三次

更加简洁一些，把两个for循环合并成一个。

Runtime: **7 ms**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    int[] result = new int[2];
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            result[0] = i;
            result[1] = map.get(complement);
            return result;
        }
        map.put(nums[i], i);
    }
    return result;
    }
}
```

---

### 第二次

利用 O\(n\)的算法来实现，整个实现步骤为：先遍历一遍数组，建立map数据，然后再遍历一遍，开始查找，找到则记录index。

Runtime: **10 ms**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int[] result = new int[2];

        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i],i);
        }

        for (int i = 0; i < nums.length; i++) {
            int t = target - nums[i];
            if (map.containsKey(t) && map.get(t) != i) {
                result[0] = i;
                result[1] = map.get(t);
                break;
            } 
        }
        return result;
    }
}
```

---

### 第一次

直接暴力解法。循环嵌入循环，遍历所有数字，找到符合的数字。

Runtime: **41 ms**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (target == nums[i] + nums[j]) {
                    result[0] = i;
                    result[1] = j;
                    break;
                }
            }
        }
        return result;
    }
}
```



