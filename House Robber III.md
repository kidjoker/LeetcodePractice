https://leetcode.com/problems/house-robber-iii/

## 解题思路
1. 使用递归的方式解决二叉树的问题 
2. 比较 当前的val加上下下层所有节点的val 和 选择 rob下一层的情况 取两者中的较大值返回
3. 因为是DFS，在从下向上回溯的过程中，会发生重复判断的情况，所有将当前执行rob函数的结果存在全局的map中，这样当出现重复调用的时候就直接返回结果即可

## 代码
```java
	private Map<TreeNode,Integer> map = new HashMap<>();
    
    public int rob(TreeNode root) {
        if(root == null){ return 0; }
        if(map.containsKey(root)){ return map.get(root); }
        int ll = root.left != null ? rob(root.left.left) : 0;
        int lr = root.left != null ? rob(root.left.right) : 0;
        int rl = root.right != null ? rob(root.right.left) : 0;
        int rr = root.right != null ? rob(root.right.right) : 0;
        
        int result = Math.max(root.val + ll + lr + rl + rr, rob(root.left) + rob(root.right));
        map.put(root,result);
        
        return result;
    }
```