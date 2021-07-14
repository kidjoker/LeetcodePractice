https://leetcode.com/problems/populating-next-right-pointers-in-each-node/

## 解题思路
1. 递归(先序)
	1. 对于每一个节点，都需要将做节点和右节点连接，同时将右节点和旁边关联的左节点连接
	2. 然后遍历下层所有左右节点
2. 双指针(层序)
	1.  使用firstNode指向当前遍历的起始节点
	2.  使用curNode指向当前遍历到的节点
	3.  每层遍历都将左右节点连接，同时将右节点和旁边节点连接(next节点存在的话)
	4. 然后修改firstNode为firstNode.left
## 代码
1. 递归
```java	
    
```
## 参考
https://youtu.be/dPCrKhwswEk
https://youtu.be/6YoQgdPZhHg