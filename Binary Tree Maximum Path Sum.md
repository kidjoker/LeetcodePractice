https://leetcode.com/problems/binary-tree-maximum-path-sum/

## 解题思路
	1. 深度优先的算法，由下至上的方向来追溯整棵树更容易理解max的计算
	2. 首先对于一颗二叉树，我们最短路径是选择左树和右树中较大的一个路径加上当前节点的值得到最大路径(参考pathMax函数的返回值)
	3. 因为如果左树或右树存在路径和小于0的情况是不需要考虑的，所以直接置为0
	4. 然后将左树+右树+当前节点的和与max做比较，得到当前的路径最大值
		1. 因为深度遍历到叶子节点返回的时候，是一层一层加上去的，所以要统计所有的和

## 代码
```java
	private int max = Integer.MIN_VALUE;
    
    public int maxPathSum(TreeNode root) {
        if(root == null){ return 0; }
        pathMax(root);
        return max;
    }
    
    private int pathMax(TreeNode root){
        if(root == null){ return 0; }
        int left = Math.max(0,pathMax(root.left));
        int right = Math.max(0,pathMax(root.right));
        
        max = Math.max(root.val+left+right,max);
        return Math.max(left,right)+root.val;
    }
```

## 参考
https://youtu.be/9ZNky1wqNUw