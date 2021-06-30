https://leetcode.com/problems/recover-binary-search-tree/

## 解题思路 [[Morrios Inorder]]
1. 使用中序遍历，理论上得到的是递增的序列，如果出现对调，必然导致序列失序（两段下降趋势）
2. 通过比较i和i+1对象的大小，我们就可以找到，用first和second来分别记录
3. 最后对调first和second所包含的值即可

## 代码
```java
	public void recoverTree(TreeNode root) {
        List<TreeNode> list = new ArrayList<>();
        inOrder(root, list);
        
        TreeNode first = null;
        TreeNode second = null;
        TreeNode firstNext = null;
        for(int i = 0; i < list.size()-1; i++){
            if(list.get(i).val > list.get(i+1).val){
                if(first == null){ first = list.get(i); firstNext = list.get(i+1); }
                else if(second == null){ second = list.get(i+1); }
            }
        }
        if(second == null){ second = firstNext; }
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
    }
    
    private void inOrder(TreeNode root, List<TreeNode> list){
        if(root == null){ return; }
        inOrder(root.left, list);
        list.add(root);
        inOrder(root.right, list);
    }
```

## 参考
https://www.cnblogs.com/grandyang/p/4297300.html