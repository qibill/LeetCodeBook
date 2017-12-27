# Add Two Numbers

### 题目

> You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
>
> You may assume the two numbers do not contain any leading zero, except the number 0 itself.

### 翻译

> 给出两个表示两个非负整数的非空链表。数字以相反的顺序存储，它们的每个节点都包含一个数字。添加两个数字，并将其作为链接列表返回。
>
> 你可以假设这两个数字不包含任何前导零，除了第0个数字本身。

### 例子

> Input: \(2 -&gt; 4 -&gt; 3\) + \(5 -&gt; 6 -&gt; 4\)  
> Output: 7 -&gt; 0 -&gt; 8  
> Explanation: 342 + 465 = 807.

---

### 第二次

不把ListNode 对象转换成 数值，直接在ListNode 对象上进行相加。**难点是cur，在栈空间上对象的传递是堆空间地址传递，并不是值传递。**

Runtime: **68 ms**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
        ListNode cur = dummy;
        int carry = 0;
        while (l1 != null || l2 != null) {
            int d1 = l1 == null ? 0 : l1.val;
            int d2 = l2 == null ? 0 : l2.val;
            int sum = d1 + d2 + carry;
            carry = sum >= 10 ? 1 : 0;
            cur.next = new ListNode(sum % 10);
            cur = cur.next;
            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }
        if (carry == 1) cur.next = new ListNode(1);
        return dummy.next;
    }  
}
```

---

### 第一次

数值可能超过int的最大范围。

**失败**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int i1 = listNodeToNumber(l1);
        int i2 = listNodeToNumber(l2);
        int sum = i1 + i2;
        return numberToListNode(sum);
    }

    public static int listNodeToNumber(ListNode l1) {
        if (l1.next == null) {
            return l1.val;
        }
        return 10 * listNodeToNumber(l1.next) + l1.val;
    }

    public static ListNode numberToListNode(int i) {

        if (i / 10 < 1) {
            ListNode ln = new ListNode(i);
            return ln;
        }
        else {
            ListNode ln = new ListNode(i % 10);
            ln.next = numberToListNode(i / 10);
            return ln;
        }
    }
}
```



