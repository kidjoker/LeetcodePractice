https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/

## 解题思路
1. 因为中序遍历，只要知道了root节点，自然知道左右子树的范围
2. 因为后序遍历，对应节点区间的最后节点就是区间的根节点
3. 所以先通过后序遍历的集合得到每个部分的根节点(从后往前)
4. 然后在中序遍历(指定范围内)中找到刚才的根节点，区分出对应的左树和右树部分
5. 重复第三步

## 代码
```java
	public TreeNode buildTree(int[] inorder, int[] postorder) {
        if(postorder == null || inorder == null || postorder.length == 0 || inorder.length == 0){ return null; }
        return helper(postorder,inorder,postorder.length-1,0,inorder.length-1);
    }
    
    private TreeNode helper(int[] postorder, int[] inorder,int postend,int instart,int inend){
        if(postend < 0 || instart > inend){ return null; }
        
        int i = instart;
        while(i <= inend){
            if(postorder[postend] == inorder[i]) break;
            i++;
        }
        
        TreeNode node = new TreeNode(postorder[postend]);
        node.left = helper(postorder,inorder,postend-(inend-i+1),instart,i-1);
        node.right = helper(postorder,inorder,postend-1,i+1,inend);
        
        return node;
    }
```