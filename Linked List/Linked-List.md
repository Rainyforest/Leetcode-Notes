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
