https://leetcode.com/problems/binary-tree-right-side-view/submissions/

## 解题思路
1. 还是层序遍历的思路，只是每次遍历的时候，不是每一个都加进去
2. 只有最后一个被添加到list里
3. 或者在递归调用的时候，先调用右孩子再调用左孩子，这样循环每一层只需要取出第一个孩子就好了

## 代码
```java
	
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        if(root == null){ return list; }
        
        helper(root, list);
        return list;
    }
    
    private void helper(TreeNode root, List<Integer> list){
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                TreeNode node = queue.poll();
                
                if(i == size-1){list.add(node.val);}
                if(node.left != null){ queue.add(node.left); }
                if(node.right != null){ queue.add(node.right); }
            }
        }
    }
```