## 2. Add Two Numbers

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

**Input:** (2 -> 4 -> 3) + (5 -> 6 -> 4)

**Output:** 7 -> 0 -> 8

## 参考
<http://geekbing.com/2016/07/27/LeetCode-2-Add-Two-Numbers/>  
<https://leetcode.com/problems/add-two-numbers/>

## 题目翻译

给你两个链表表示两个非负整数。链表中的数字按照相反的顺序存储，并且每个节点只包含一个数字。将两个数字相加并返回结果链表。

## 解题思路
1. 数字存储是反向的，即整数123按照题目中的链表表示为（3 －> 2 －> 1）
2. 题目给的例子恰好有歧义，题目并没有说给出的两个链表长度相同。所以较长的链表后面的值应顺接在结果后面，比如：(1 -> 2) + (2 -> 3 -> 4)的结果应为(3 -> 5 -> 4)
3. 如果两个链表最后节点相加结果有进位，最终结果应该将进位单独算作一个节点，比如： (2 -> 7) + (9 -> 2)的结果应为(1 -> 0 -> 1)

创建dummyList新链表，用于返回结果，创建curr链表指向dummyList
```
var dummyList = new ListNode(0);
var curr = dummyList;
```

计算两个链表头部的和。sum用来计算每一次的和（对应的进位，l1节点的值，l2节点的值。由于第一次进位为0，所以只需要计算两个链表表头的和）需判断链表中的值是否存在
```
x = (l1 !== null) ? l1.val : 0;
y = (l2 !== null) ? l2.val : 0;
sum = carry + x + y;
```
计算进位，值为0或1，Math.floor()向下取整
```
carry = Math.floor(sum / 10); 
```

创建新的节点，把计算结果保存到新节点，值为0-9。curr指针向后移动。
```
curr.next = new ListNode(sum % 10);//插入新节点
curr = curr.next;
```

如果非空，`l1`和`l2`指向下一节点，用于后面移动读取数值
```
if (l1 !== null) l1 = l1.next;
if (l2 !== null) l2 = l2.next;
```

返回新链表。因为保留有头节点，所以返回.next
```
return dummyList.next;
```

## AC Code
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
function ListNode(val) {
     this.val = val;
     this.next = null;
};
var addTwoNumbers = function(l1, l2) {
    var dummyList = new ListNode(0);
    var curr = dummyList;
    var carry = 0, x, y, sum;
    while(l1 !== null || l2 !== null || carry){
    	x = (l1 !== null) ? l1.val : 0;
    	y = (l2 !== null) ? l2.val : 0;
    	sum = carry + x + y;
    	//进位
    	carry = Math.floor(sum / 10);  
    	curr.next = new ListNode(sum % 10);//插入新节点
    	curr = curr.next;
    	if (l1 !== null) l1 = l1.next;
        if (l2 !== null) l2 = l2.next;
    } 
    return dummyList.next;
};
```
