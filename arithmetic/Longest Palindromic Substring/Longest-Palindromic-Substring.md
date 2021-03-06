# 解题思路
> 这一道题使用到的是Manacher’s算法

* 因为回文子串长度有奇数和偶数2种情况,为了方便期间,要对字符串进行预处理

如'abc' -> '#a#b#c#d#',这样的话无论字符串长度是奇数还是偶数经过处理后都会变成奇数

* 但在这里还要在新字符串前面加上一个特殊字符比如'$',防止数组越位,看到后面的代码你就明白了

## 算法的核心思想

* 我们用一个数组`strArr`来存放新字符串中的每一个字符
* 用数组`r`来存放对应字符的回文半径

下面是一个例子

|i|0|1|2|3|4|5|6|7|8|9|10|11
|---|---|---|---|---|---|---|---|---|---|---|---|---
|strArr[i]|$|#|a|#|c|#|a|#|b|#|c|#
|r[i]|0|0|1|0|3|0|1|0|1|0|1|0

* 只要你能得到这样的数据那么就能很轻松的得到最长回文子串了,下面介绍详细步骤


1. 我们用变量`center`表示当前最长子串的对称中心,用`maxR`表示当前子串的右边界,初始值都为0
2. 从索引i为1开始遍历数组strArr
3. 如果`i > maxR`说明strArr[i]不在当前最长回文子串中,则`r[i] = 0`
4. 如果`i <= maxR`说明strArr[i]在当前最长回文子串中,则`r[i] = Math.min(maxR - i, r[2 * center - i])`. 这里这样做是因为要分2种情况:1是以r[i]为中心的回文子串正好被包括在当前最长回文子串中,所以用`r[2 * center - i]`表示相对于`center`对称的回文半径,因为以及计算过了,而且它们的值一定相同;2是以r[i]为中心的回文子串超过了边界,因为超过部分还未计算,所以只能先用`maxR - i`表示为边界内的部分.
5. 之后从中心扩散得到回文半径
6. 最后更新下`center`和`maxR`的值
