### 题目
#Leetcode 
https://leetcode.com/problems//

### 解题思路
递归到每一个叶子节点，计算当前节点数是否小雨全局变量min


### 代码
```java
	private int min = Integer.MAX_VALUE;
    
    public int minDepth(TreeNode root) {
        if(root == null){ return 0; }
        
        helper(root,0);
        return min;
    }
    
    private void helper(TreeNode root, int curMin){
        if(root == null){ return; }
        
        curMin++;
        if(root.left == null && root.right == null){
            min = (curMin < min) ? curMin : min;
        }
        
        if(root.left != null){ helper(root.left,curMin); }
        if(root.right != null){ helper(root.right,curMin); }
        curMin--;
    }
```

### 参考