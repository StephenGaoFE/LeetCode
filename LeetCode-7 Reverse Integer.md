# LeetCode-7 Reverse Integer

## 题目
Reverse digits of an integer.  

Have you thought about this?
Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!  

If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.  

Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?  

For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.    

## Example:

```js
Example1: x = 123, return 321  
Example2: x = -123, return -321 
```

## 参考
<http://geekbing.com/2016/07/28/LeetCode-7-Reverse-Integer/>  
<https://leetcode.com/problems/reverse-integer/>


## 题目翻译

翻转字符串
在写代码之前，你考虑过下面的这些问题吗？

假如数字的最后一位是0，应该输出什么呢？例如10，100。

你注意到反转整数可能会导致溢出吗？假设输入是32位的整数（范围是-2147483648到2147483647），反转整数1000000003得到的结果3000000001会导致溢出。你应该如何处理这种情况呢？

对于上面的情况，当反转整数发生溢出的时候，你的函数应该返回0。

## 解题思路
小心注意别掉坑里了，本题会有溢出的可能，结果需要控制在Int32范围内，即（-2147483648到2147483647）
```math
 -2^{32} < res <  2^{32} 
```
利用JS的toString(),split(),reverse().join()方法，3行代码搞定^^

## AC Code
```js
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    var res = (Math.abs(x).toString()).split("").reverse().join("");
    res *= (x >= 0) ? 1: -1;
    return (res >= -2147483648 && res <= 2147483647) ? res : 0;
};
console.log(reverse(123));
console.log(reverse(-123));
```
