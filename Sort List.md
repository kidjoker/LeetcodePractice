# Sort List
#每日技术

### 题目
Given the head of a linked list, return the list after sorting it in ascending order.
Follow up: Can you sort the linked list in O(n logn) time and O(1) memory (i.e. constant space)?

### 解题思路
将链表切分为一个的单独node，然后两两merge，因为只有最多一个节点，所以merge相对简单，然后递归回上一层，再进行merge，直到所有元素都有序为止

### 代码
```java
	public ListNode sortList(ListNode head) {
        if(head == null || head.next == null){ return head; }
        ListNode slow = head;
        ListNode fast = head;
        ListNode pre = head;
        
        while(fast != null && fast.next != null){
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        
        pre.next = null;
        
        return merge(sortList(head),sortList(slow));
    }
    
    private ListNode merge(ListNode left, ListNode right){
        ListNode dummyHead = new ListNode(-1);
        ListNode cur = dummyHead;
        
        while(left != null && right != null){
            if(left.val < right.val){
                cur.next = left;
                cur = left;
                left = left.next;
            }
            else{
                cur.next = right;
                cur = right;
                right = right.next;
            }
        }
        
        if(left != null){
            cur.next = left;
        }
        if(right != null){
            cur.next = right;
        }
        
        return dummyHead.next;
    }
```

### 参考资料
https://youtu.be/M1TwY0nsTZA