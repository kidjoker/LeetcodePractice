# Insertion Sort List
#每日技术

### 题目
Given the head of a singly linked list, sort the list using insertion sort, and return the sorted list's head.
The steps of the insertion sort algorithm:
	1	Insertion sort iterates, consuming one input element each repetition and growing a sorted output list.
	2	At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list and inserts it there.
	3	It repeats until no input elements remain.
The following is a graphical example of the insertion sort algorithm. The partially sorted list (black) initially contains only the first element in the list. One element (red) is removed from the input data and inserted in-place into the sorted list with each iteration.

### 解题思路
	1. 插入排序的思想
	2. 从前到后遍历到倒数第二个节点，如果当前元素比后一个元素小就跳过
	3. 都则从头开始往后遍历，cur.next元素应该放在哪一个位置，然后插入到合适的位置

### 代码
```java
	public ListNode insertionSortList(ListNode head) {
        if(head == null || head.next == null){ return head; }
        
        ListNode dummyHead = new ListNode(-1);
        dummyHead.next = head;
        
        ListNode cur = head;
        ListNode prev = null;
        ListNode temp = null;
        
        while(cur != null && cur.next != null){
            if(cur.val <= cur.next.val){ cur = cur.next; }
            else{
                temp = cur.next;
                cur.next = cur.next.next;
                prev = dummyHead;
                while(prev.next.val <= temp.val){
                    prev = prev.next;
                }
                
                temp.next = prev.next;
                prev.next = temp;
            }
        }
        
        return dummyHead.next;
    }
```

### 参考资料
https://youtu.be/N1VVLLan6S0