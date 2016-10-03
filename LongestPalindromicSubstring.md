## 题目
最长的回文子串(动态规划)  
abbbba # 就是一个回文字符串    
cabbbbaf # 最长的回文字符串就是abbbba

## 参考
https://leetcode.com/problems/longest-palindromic-substring/  
http://blog.csdn.net/soszou/article/details/37312317
## 思路

假设dp[ i ][ j ]的值为true，表示字符串s中下标从 i 到 j 的字符组成的子串是回文串。那么可以推出：  
dp[ i ][ j ] = dp[ i + 1][ j - 1] && s[ i ] == s[ j ]。  
这是一般的情况，由于需要依靠i+1, j -1，所以有可能 i + 1 = j -1, i +1 = (j - 1) -1，因此需要求出基准情况才能套用以上的公式：  
a. i + 1 = j -1，即回文长度为1时，dp[ i ][ i ] = true;  
b. i +1 = (j - 1) -1，即回文长度为2时，dp[ i ][ i + 1] = （s[ i ] == s[ i + 1]）。  
有了以上分析就可以写出代码了。需要注意的是动态规划需要额外的O(n2)的空间。
## AC
```
package com.LeetCode;
//最长的回文子串(动态规划)
//abbbba # 就是一个回文字符串  
//cabbbbaf # 最长的回文字符串就是abbbba

public class LongestPalindromicSubstring {
	public static String longestPalindrome(String s) {
		int length = s.length();
		if(length < 2 ) return s;
		// 状态表 
		boolean [][]P = new boolean[length][length];//默认false
        int start = 0, end = 0; // 最长回文字符串开始字符的索引 
        String longestStr = null;
        int maxLength = 0; // 最长回文字符串的长度 
        for(int i=0; i < length; i++) {
            // 第 i 个 到 i 个必然是回文的
            P[i][i] = true;
        }
        for(int i=0; i <= length-2; i++){
        	// 判断相邻两数是否相等，若相等，便是回文字符串的初始条件
            if(s.charAt(i) == s.charAt(i+1)) {
                P[i][i+1] = true;
                //longestStr = s.substring(i,i+2);
                 start = i;
                 end = i+1;
            }
        }
        
        //接下来讨论回文长度3以上
        for(int len = 3; len <= length; len++){
        	for(int i=0; i <= length-len; i++){
        		int j = i + len - 1;
        		if (s.charAt(i) == s.charAt(j)) {  
        			P[i][j] = P[i+1][j-1];
        			if(P[i][j] == true && len > maxLength){
        				//longestStr = s.substring(i,j+1);
        				start = i;
        				end = j;
        			}
        		}
        	}
        }
        longestStr = s.substring(start,end+1);
        return longestStr;
    }
	public static void main(String[] args) {
		String s1 = "abcdcba";
		//String s2 = "xabbbbac";
		System.out.println(longestPalindrome(s1));
	}
	
}

```
