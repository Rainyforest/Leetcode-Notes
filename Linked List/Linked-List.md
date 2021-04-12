### Tips
-  2 pointer 

### [Remove-duplicates-from-sorted-list](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)
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
    public ListNode deleteDuplicates(ListNode head) {
        ListNode pos = head;
        while(pos != null){
            ListNode curr = pos;
            while(curr.next!=null && curr.next.val==pos.val){
                curr = curr.next;
            }
            pos.next = curr.next;
            pos = pos.next;
        }
        return head;
    }
}
```
improved version
```
public ListNode deleteDuplicates(ListNode head) {
    ListNode current = head;
    while (current != null && current.next != null) {
        if (current.next.val == current.val) { // only need one loop
            current.next = current.next.next;
        } else {
            current = current.next;
        }
    }
    return head;
}
```

### [Rotate-list](https://leetcode.com/problems/rotate-list/)
```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null) return head;
        int len = 0;
        ListNode curr1 = head;
        for(curr1 = head; curr1.next != null; curr1 = curr1.next){
            len ++;
        }
        len ++;
        k %= len;
        if(k == 0)return head;
        int counter = 0;
        ListNode curr2 = head;
        for(curr2 = head; counter < len - k - 1; curr2 = curr2.next){
            counter ++;
        }
        ListNode newHead = curr2.next;
        curr2.next = null;
        curr1.next = head;
    
        return newHead;
    }
}
```
