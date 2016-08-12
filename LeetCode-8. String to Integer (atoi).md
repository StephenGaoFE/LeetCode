# LeetCode-8. String to Integer (atoi)

## 题目
Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

Requirements for atoi:
The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.



## Example:

```js
null
```

## 参考
 
<https://leetcode.com/problems/string-to-integer-atoi/>


## 题目翻译
题目太长了，懒得翻译了= =  
大概意思是字符串转成整数，符合atoi规则


## 解题思路
百度百科：
> atoi (表示 ascii to integer)是把字符串转换成整型数的一个函数，应用在计算机程序和办公软件中。
atoi( ) 函数会扫描参数 nptr字符串，跳过前面的空白字符（例如空格，tab缩进等，可以通过isspace( )函数来检测），直到遇上数字或正负符号才开始做转换，而再遇到非数字或字符串结束时('\0')才结束转换，并将结果返回。如果 nptr不能转换成 int 或者 nptr为空字符串，那么将返回 0

说人话：  
字符串转整数，自动去掉空格，支持正负号，当字符串总检测到非数字时，中断检测并返回结果，超出Int32范围的就显示最大（小）值。

坑1：去除字符串左右空格，中间的不能去掉！把中间的空格也去掉就挂了啊  
以下是比较恶心人的Test case：  
"+0 123"   return:0（而不是123）  
"-123a2"   return:-123  
"+—123 "   return:0  

## AC Code
```js
/**
 * @param {string} str
 * @return {number}
 */

var myAtoi = function(str) {
	var sign = 1;
    var res = 0;
	if(str.length === 0 || str === null){
		return 0;
	}
	str = str.trim();//去除字符串左右空格，中间的不能去掉！
	//str = str.replace(/^\s+|\s+$/g,"");
	str = str.split("");
	
	if(str[0] === "+"){
		str.shift();//去除数组第一个元素
	}else if(str[0] === "-"){
		str.shift();
		sign = -1;//判断正负
	}
	//str.charCodeAt(n)字符串中第n个字符转化成ascii代码
	//str.charAt(n)返回字符串中index=n的字符
	//parseInt(str,[x]) 把字符串转换为整数，x=10为10进制（可选）
	for(var i=0; i< str.length; i++){
		if(str[i].charCodeAt() >= 48 && str[i].charCodeAt() <= 57){
			res = res*10 + parseInt(str[i]);
		}else{
			break;
		}
	}
    //超出Int32范围，返回Int32最大/小值
    res = (res !== 0) ? res *= sign : res;
    res = res > 2147483647 ? 2147483647 : res;
    res = res < -2147483648 ? -2147483648 : res;
    return res;
};

console.log(myAtoi("  +0 123"));
```
