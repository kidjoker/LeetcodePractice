https://leetcode.com/problems/kth-smallest-element-in-a-bst/

## 解题思路
1. 首先不断向左子节点寻找，将节点放到stack中
2. 然后弹出一个节点，如果当前k=1表明就是我要的节点
3. 否则递归遍历右节点，因为右边也需要不断向左节点寻找，放到stack之中，因为已经弹出一个较小的node，所以递归传入k-1

## 代码
```java
	private Stack<TreeNode> stack = new Stack<>();
    
    public int kthSmallest(TreeNode root, int k) {
        TreeNode node = root;
        while(node != null){
            stack.push(node);
            node = node.left;
        }
        
        node = stack.pop();
        if(k == 1){ return node.val; }
        return kthSmallest(node.right, k-1);
    }
```