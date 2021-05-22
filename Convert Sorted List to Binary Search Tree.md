# Convert Sorted List to Binary Search Tree
#每日技术

### 题目
Given the head of a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.
For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1

### 解题思路
因为链表是有序的，所有题目转变成不断找中点，然后迭代左边节点形成左子树和右边节点形成右子树，然后下一层继续迭代下下一层，直到元素都没有为止

### 代码
```java
	public TreeNode sortedListToBST(ListNode head) {
        if(head == null) { return null; }
        return helper(head,null);
    }
    
    private TreeNode helper(ListNode head, ListNode tail){
        if(head == tail){ return null; }
        ListNode slow = head;
        ListNode fast = head;
        
        while(fast != tail && fast.next != tail){
            slow = slow.next;
            fast = fast.next.next;
        }
        
        TreeNode node = new TreeNode(slow.val);
        node.left = helper(head,slow);
        node.right = helper(slow.next,tail);
        return node; 
    }
```

### 参考资料
https://youtu.be/aH0rBLZLr2E