**难度简单**

给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

**示例 1：**

```javascript
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

**注意:**  

- 无

**我的解题思路**

1. 俩次循环验证 i + j 是否等于 目标值

  **我的答案**

```
var twoSum = function(nums, target) {
    let arr = [];
    let length = nums.length
    for (let i = 0; i< length; i++) {
        for(let j = i + 1; j < length; j++) {
            if(nums[i] + nums[j] === target) {
                arr = [i, j]
                break
            }
        }	
    }
        return arr
};
```

这算是一种最笨的办法了吧, 运行结果稍慢些

后来经过一些想法有了另一种答案 就是做一层映射

**另一种思路**

   1 .最开始遍历nums 做一层映射 maps maps的key 就是当前值 value 是索引

2. 第二次遍历 直接用target - nums[i] 可以得到如果i + 什么值可以得到target 
3. 通过这个结果去maps 里面查找 是否存在对应的key 且值不等于i  就将这个结果放入result 数组

**另一种答案**

```
var twoSum = function(nums, target) {
    var maps = {}, result = []
    for (let i = 0 ; i < nums.length; i++) {
        maps[nums[i]] = i
    }
    for (let i = 0 ; i < nums.length; i++) {
        var num = target - nums[i]
        if(maps[num] && maps[num] !== i) {
            result = [i , maps[num]]
        }
    }
    return result
}

```

俩种方法结果相同都可以通过leetcode 的测试 

其中第一种最快达到180ms 第二种 基本在100ms 左右 足以得出第二种算法是会比第一种快很多的 但是内存消耗会比第二种多出2M 左右 