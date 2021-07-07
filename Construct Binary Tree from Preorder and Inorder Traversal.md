https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

## 解题思路
1. 因为中序遍历，只要知道了root节点，自然知道左右子树的范围
2. 因为先序遍历，对应节点区间的第一个节点就是区间的根节点
3. 所以先通过先序遍历的集合得到每个部分的根节点
4. 然后在中序遍历(指定范围内)中找到刚才的根节点，区分出对应的左树和右树部分
5. 重复第三步

## 代码
```java
	public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder == null || inorder == null || preorder.length == 0 || inorder.length == 0){ return null; }
        return helper(preorder,inorder,0,0,inorder.length);
    }
    
    private TreeNode helper(int[] preorder, int[] inorder,int prestart,int instart,int inend){
        if(prestart >= preorder.length || instart > inend){ return null; }
        
        int i = instart;
        while(i < inend){
            if(preorder[prestart] == inorder[i]) break;
            i++;
        }
        
        TreeNode node = new TreeNode(preorder[prestart]);
        node.left = helper(preorder,inorder,prestart+1,instart,i-1);
        node.right = helper(preorder,inorder,prestart+(i-instart+1),i+1,inend);
        
        return node;
    }
```