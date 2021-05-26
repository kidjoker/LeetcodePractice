# Reorder List
#每日技术

### 题目
You are given the head of a singly linked-list. The list can be represented as:
L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

### 解题思路
	1. 首先需要使用快慢指针，将链表分为两段
	2. 将后面一段进行reverse
	3. 然后类似一上一下的方式，merge两个链表即可

### 代码
```java
	public void reorderList(ListNode head) {
        if(head == null || head.next == null) return;
        ListNode l2 = null;
        
        ListNode slow = head;
        ListNode fast = head;
        ListNode prev = null;
        
        while(fast != null && fast.next != null){
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        
        prev.next = null;
        l2 = slow;
        
        l2 = reverse(l2);
        merge(head,l2);
    }
    
    private ListNode reverse(ListNode node){
        ListNode currentNode = node;
        ListNode prevNode = null;
        
        while(currentNode != null){
            ListNode nextNode = currentNode.next;
            currentNode.next = prevNode;
            prevNode = currentNode;
            currentNode = nextNode;
        }
        
        return prevNode;
    }
    
    private void merge(ListNode l1, ListNode l2){
        while(l1 != null){
            ListNode l1Next = l1.next;
            ListNode l2Next = l2.next;
            
            l1.next = l2;
            if(l1Next == null){
                break;
            }
            l2.next = l1Next;
            
            l1 = l1Next;
            l2 = l2Next;
        }
    }
```

### 参考资料
https://youtu.be/xRYPjDMSUFw