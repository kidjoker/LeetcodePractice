https://leetcode.com/problems/validate-binary-search-tree/

## 解题思路
1. 二叉搜索树的特点：左边的节点都比当前节点小；右边的节点都比当前节点大
2. 所以如果出现第一个一个比当前节点小，一个比当前节点大，那一定是最靠近的公共祖先
3. 否则，如果都比当前节点小则向左孩子靠近，否则靠近右孩子

## 代码
```java
	public boolean isValidBST(TreeNode root) {
        return isValidBST(root, null, null);
    }
  
    private boolean isValidBST(TreeNode root, Integer min, Integer max) {
        if (root == null) return true;
        if ((min != null && root.val <= min) ||(max != null && root.val >= max))
            return false;
 
        return isValidBST(root.left, min, root.val) && isValidBST(root.right, root.val, max);
	}
```