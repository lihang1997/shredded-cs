## 24.两两交换链表中的节点

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

 

示例:

给定 1->2->3->4, 你应该返回 2->1->4->3.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/swap-nodes-in-pairs
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

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
  public ListNode swapPairs(ListNode head) {
    ListNode dummy = new ListNode(-1);
    dummy.next = head;
    ListNode pre = dummy; //下两个节点的前节点

    while (pre.next != null && pre.next.next != null) {
      //实在搞不清楚一堆next，就分别命名保存为临时变量
      ListNode n3 = pre.next.next.next; //3
      ListNode n2 = pre.next.next; //2
      ListNode n1 = pre.next; //1
      n1.next = n3;
      n2.next = n1;
      pre.next = n2;
      
      pre = n1; //下两个节点的前节点
    }
    return dummy.next;
  }
}
```



## 25.K个一组翻转链表

给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

 

示例：

给你这个链表：1->2->3->4->5

当 k = 2 时，应当返回: 2->1->4->3->5

当 k = 3 时，应当返回: 3->2->1->4->5

 

说明：

你的算法只能使用常数的额外空间。
你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-nodes-in-k-group
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

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
	public ListNode reverseKGroup(ListNode head, int k) {
    if (head == null || head.next == null || k <= 1) {
      return head; //没有必要反转
    }
		ListNode dummy = new ListNode(-1);
    dummy.next = head;
    ListNode pre=dummy, next=null, cur=head; //pre为kGroup前序节点，next为kGroup后续节点
    while (cur != null) {
      int i;
      for (i=0; i<k && cur != null; i++) {
        next = cur.next;
        cur = next;
      }
      if (i == k) { //反转
        ListNode newHead = reverse(pre.next, next);
        ListNode tmp = pre.next;
        pre.next.next = next; //接尾部
        pre.next = newHead; //接头部
        pre = tmp;
      } else {
        break;
      }
    }
    return dummy.next;
  }
  
  //指定起止节点反转
  private ListNode reverse(ListNode start, ListNode end) {
    ListNode pre=null, next;
    while (start != end) {
      next = start.next;
      start.next = pre;
      pre = start;
      start = next;
    }
    return pre;
  }
}
```

