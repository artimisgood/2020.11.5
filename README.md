# 2020.11.5————合并两个有序链表
## 题目

将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：
```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```
## 解题一
### 语言
java
### 思路
```
merge=
{ 
list1[0]+merge(list1[1:],list2)  list1[0]<list2[0]
list2[0]+merge(list1,list2[1:])  otherwise
}
```
将每个链表里面较小的节点插到另一个节点上
### 代码
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1==null){
            return l2;//如果l1为空返回l2
        }
        else if(l2==null){
            return l1;//如果l2为空返回l1
        }
        else if(l1.val<l2.val){
            l1.next = mergeTwoLists(l1.next,l2);//如果此时l1的节点小那就将l1这个节点与另一个合并
            return l1;
        }
        else{
            l2.next = mergeTwoLists(l2.next,l1);//同上
            return l2;
        }
    }
}
```
## 解题二
### 语言 
java
### 思路
迭代法：

还是比较每个节点，不过要设置四个指针进行链接。

- prehead是头节点，用来输出，注意要加next。
- prev用来遍历链表进行链接
- l1用来指向l1链表
- l2用来指向l2链表

![](https://assets.leetcode-cn.com/solution-static/21/5.PNG)
![](https://assets.leetcode-cn.com/solution-static/21/6.PNG)
![](https://assets.leetcode-cn.com/solution-static/21/7.PNG)
![](https://assets.leetcode-cn.com/solution-static/21/8.PNG)

### 代码
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode prehead = new ListNode(-1);//创建一个哨兵节点作为头

        ListNode prev = prehead;//创建一个遍历节点,一开始指向头
        while(l1!=null&&l2!=null){
            if(l1.val<=l2.val){
                prev.next = l1;
                l1 = l1.next;
            }else{
                prev.next = l2;
                l2 = l2.next;
            }
            prev = prev.next;//连接
        }

        //合并后肯定有个没合并完，这时候要判断
        prev.next=l1==null?l2:l1;

        return prehead.next;//头节点注意要加next
    }
}
```
