**难度简单**

重复出现的子串要计算它们出现的次数。给定一个字符串s,计算具有相同数量0和1的非空连续字符串的数量,并且这些字符串中的所有0和所有1都是组合在一起的

**示例 1：**

```javascript
输入: "00110011"
输出: 6
解释: 有6个子串具有相同数量的连续1和0：“0011”，“01”，“1100”，“10”，“0011” 和 “01”。

请注意，一些重复出现的子串要计算它们出现的次数。

另外，“00110011”不是有效的子串，因为所有的0（和1）没有组合在一起。
```

**注意:**  

* `s.length` 在1到50,000之间。
* `s` 只包含“0”或“1”字符。

**我的解题思路**

借助了leetcode上某大神的想法有了自己的思路

1.   声明三个变量  
   * pre = 0 记录上一个值出现的次数
   * current = 1 记录当前值出现的次数 因为会判断i === i+ 1 本质会缺少1位 所以current 初始值位1
   * result = 0  记录所有符合条件出现的次数
2.  循环判断 i 和 i+1 是否相等 如果相等 则current 加 1  如果不等 则将 pre 赋值位 current  current 重新赋值为1  这里current 赋值为1的原因是将这次结果也并入计算
3. 在循环体内 判断 pre >= current 如果符合条件 则 result ++  `注释>=的原因是因为如果上一个值 >= 当前值则一定成立为俩种情况 比如 001  就存在01符合条件的值 0011就符合条件`
4. 最后return result  

  **我的答案**

```
var countBinarySubstrings = function(s) {
    var pre = 0;  var current = 1 ; var result = 0;
    for (var i = 0, len = s.length - 1;  i<len ; i++) {
        if (s[i] === s[i + 1]) {
            current++
        } else {
            pre = current
            current = 1
        }
        if (pre  >= current) {
            result ++
        }

    }
    return result

};
countBinarySubstrings("00110")
```

**慕课网算法老师思路**

   1 . 定义方法 match 参数 str 。

2.  match 方法 第一步 match加正则找出首先出现0或1的所有数量  j 
3. match 方法第二步 将j[0] 取反 比如 1 就取 0,0就取1  然后根据j的长度 执行 repeat方法 得到 o
4. 实际上得出的结果就是 j + o
5. 设置正则表达式 验证传入的参数是否符合j+0的规则 如果是返回符合规则的字符串
6. 循环遍历字符串 调用match方法 传入的参数是 截取当前字符串 0 ， i
7.  如果成功向数组添加一条 返回这个数组

**老师答案**

```
export default (str) => {
  // 建立数据结构，堆栈，保存数据
  let r = []
  // 给定任意子输入都返回第一个符合条件的子串
  let match = (str) => {
    let j = str.match(/^(0+|1+)/)[0]
    let o = (j[0] ^ 1).toString().repeat(j.length)
    let reg = new RegExp(`^(${j}${o})`)
    if (reg.test(str)) {
      return RegExp.$1
    } else {
      return ''
    }
  }
  // 通过for循环控制程序运行的流程
  for (let i = 0, len = str.length - 1; i < len; i++) {
    let sub = match(str.slice(i))
    if (sub) {
      r.push(sub)
    }
  }
  return r
}

```

