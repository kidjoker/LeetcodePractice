https://leetcode.com/problems/serialize-and-deserialize-binary-tree/submissions/

## 解题思路

## 代码
```java
	public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        buildStringBuilder(root,sb);
        return sb.toString();
    }
    
    private void buildStringBuilder(TreeNode root,StringBuilder sb){
        if(root == null){
            sb.append("#").append(",");
        }
        else{
            sb.append(root.val).append(",");
            buildStringBuilder(root.left,sb);
            buildStringBuilder(root.right,sb);
        }
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if(data == null){ return null; }
        String[] dataArr = data.split(",");
        Queue<String> queue = new LinkedList<>();
        Collections.addAll(queue,dataArr);
        return buildTree(queue);
    }
    
    private TreeNode buildTree(Queue<String> queue){
        if(queue.isEmpty()){ return null; }
        String element = queue.poll();
        if(element.equals("#")){ return null; }
        
        TreeNode node = new TreeNode(Integer.parseInt(element));
        node.left = buildTree(queue);
        node.right = buildTree(queue);
        return node;
    }
```

## 参考
https://www.youtube.com/watch?v=cLsWdZd90j8