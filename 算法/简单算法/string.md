**难度简单**

给定一个字符串,你需要反转字符串中每个单词的字符顺序,同时仍保留空格和单词的初始顺序。

**示例 1：**

```javascript
输入: "Let's take LeetCode contest"
输出: "s'teL ekat edoCteeL tsetnoc"
```

**注意:**  在字符串中, 每个单词由单个空格分隔,  并且字符串中不会有任何额外的空格。

**我的解题思路**

1.将字符串根据空格截取成数组, 变成以下结果

["Let's","take","LeetCode", "contest"]

2.将数组循环 得到数组中每一个字符串。 由于字符串是无法执行JS的反转方法 reverse 所以将循环的每一项通过split('')转为数组执行reverse()然后在通过join(''')转为字符串通过上述方法可将结果转化为

```javascript
["s'teL", "ekat"，"edoCteeL" ， "tsetnoc"]
```

3. 将得到得结果转为通过join('  ')转为字符串 即可完成此题

  **我的答案**

```
function revreseStr(s) {
    var t = s.split(' ')
    var e = [].concat(t)
    for(let i = 0, len = e.length ; i < len; i++) {
        e[i] = e[i].split('').reverse().join('')
    }
    return e.join(' ')
}
```

**慕课网算法老师思路**

跟我的想法差不多

**老师答案**

```
export default (str) => {
    let arr = str.split(' ')
    let result = arr.map(item => {
        return item.split('').reverse().join('')
    })
    return result.join(' ')
}
```

