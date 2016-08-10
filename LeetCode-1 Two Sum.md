# LeetCode-1 Two Sum
为了应对面试中可能会出现的在线编程题，虽然不太情愿，我也随大流开始进入LeetCode刷题模式。由于本人编程水平有限，打算先从最简单的题开始。  
大家刷题大多都用的Java或者C，作为一个Web前端，常用的语言当然是Javascript咯。  
由于JS执行效率低，又没有块作用域，写起来经常会报一些奇怪的错误，用JS写数据结构和算法的难度是大于Java的，用Javascript写个链表，那画面简直太美XD  
因此，本博客开始连载小众的**Javascript**刷题，保证你在别的地方没见过！（至于能连载多少期那就随缘吧） 

## 题目
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution.

## Example:

```js
Given nums = [2, 7, 11, 15], target = 9,
			
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## 参考
<http://geekbing.com/2016/07/27/LeetCode-1.%20Two%20Sum/>  
<https://leetcode.com/problems/two-sum/>


## 题目翻译

给定一个整数的数组，要求返回两个整数的下标（这两个整数相加得到一个给定的目标值）。  
你可以假设对于每一组输入有且仅有一个特定的解决方案。

## 解题思路
二重循环，穷举算法（我只会这种笨办法），两个值相加等于目标值时，返回数组中的index。

## AC Code
```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    for(var i=0; i<nums.length; i++){
    	for(var j=i+1; j<nums.length; j++){
    		if(nums[i]+nums[j] == target){
    			return [i,j];
    			}
    		}
    }
    return 0;
};
var res = twoSum([2, 7, 11, 15], 9);
console.log(res);
```
