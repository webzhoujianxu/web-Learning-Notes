**难度简单**

假设你有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花卉不能种植在相邻的地块上，它们会争夺水源，两者都会死去。

给定一个花坛（表示为一个数组包含0和1，其中0表示没种植花，1表示种植了花），和一个数 **n** 。能否在不打破种植规则的情况下种入 **n** 朵花？能则返回True，不能则返回False。

**示例 1：**

```javascript
输入: flowerbed = [1,0,0,0,1], n = 1
输出: True
```

**示例 2：**

```
输入: flowerbed = [1,0,0,0,1], n = 2
输出: False
```

**注意:**  

- 数组内已种好的花不会违反种植规则。
- 输入的数组长度范围为 [1, 20000]。
- **n** 是非负整数，且不会超过输入数组的大小。

**我的解题思路**

1. 寻找连续三个及以上的0
2. 注意边界情况在数组最开始与数组最后分别添加一个0
3. 在循环内如果 i !== 0 则执行computed 计算函数 如果等于3则直接加1 如果小于3 说明无法放置花

   如果 > 3  分为多种情况 比如结果为5就可以放置2朵 7则3朵 结果为6就可以放2朵 4则1朵   所以分俩种情况计算   用出现的数量cur - 3 后在比余2 看比余是否等于0 若果等于0 则  count+=((cur - 3) / 2) + 1

​    如果比余不为0    count += Math.ceil((cur - 3) / 2)

  **我的答案**

```
var canPlaceFlowers = function(flowerbed, n) {
   flowerbed.push(0)
    flowerbed.unshift(0)
    var count = 0;
    var cur = 1;
    var computed = function () {
        if (cur === 3) {
            count ++
            cur = 1
        }  else if (cur > 3) {
            var nums = (cur - 3) % 2
            if (nums === 0) {
                count += ((cur - 3) / 2) + 1
                cur = 1
            }  else {
                count += Math.ceil((cur - 3) / 2)
                cur = 1
            }
        } else {
            cur = 1
        }
    }
    for (var i = 0 ; i <flowerbed.length; i++ ) {
        if (flowerbed[i] === 0) {
            if (flowerbed[i] === flowerbed[i+1]) {
                cur++
            }
        }  else {
            computed ()
        }
        if (i === flowerbed.length - 1) {
            computed()
        }
    }
   return n <= count
};
console.log(canPlaceFlowers([1,0,0,0,1,0,0],2))
```

这是在看老师课程之前的出来的答案。 感觉自己的答案比较繁琐. 稍后对比下老师的答案总结一下问题所在。

**另一种思路**

1. 好吧 视频的代码有些问题跑不通leetcode 大致的想法理解了 结合老师的想法重新出一个答案
2. 边界情况依然向数组前和数组后各加一个0做处理
3. 每次判断 当前i 和 当前I的前一位和后一位 是否等于0 如果满足条件sum++ 这里需要i++一次 原因自己参考下就知道了。

**另一种答案**

```
var canPlaceFlowers = function(flowerbed, n) {
    let sum = 0;
    flowerbed.unshift(0)
    flowerbed.push(0)
    for (let i = 0, len = flowerbed.length -1 ; i < len;i++) {
        if(flowerbed[i] === 0) {
            if(flowerbed[i+1] === 0&&flowerbed[i-1] === 0) {
                sum ++
                i++
            }
        }
    }
    return sum >= n
};
```

俩种方法结果相同都可以通过leetcode 的测试 

第二种相对更省时间也更简单 其实刚开始也想到了。不过第一种自己更快的想到了,就先写完了 。  看来以后还是要三思而后行啊