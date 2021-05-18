# Triangle
#每日技术

### 题目
Given a triangle array, return the minimum path sum from top to bottom.
For each step, you may move to an adjacent number of the row below. More formally, if you are on index i on the current row, you may move to either index i or index i + 1 on the next row.

### 解题思路
	1. 当前节点的最小值和下一层的两个节点有关系，这种先后节点有关联的题目都应该联想到DP
	2. 我们使用从下至上的方式来解题，首先是要9哦那个dp数据来存储最下层的所有节点，然后向上追一层，dp[i]等于下层的Math.min(dp[i],dp[i+1])加上当前节点的值
	3. 然后我们继续向上递推，知道到达最上层的节点退出即可
### 代码
```java
	public int minimumTotal(List<List<Integer>> triangle) {
        int[] dp = new int[triangle.size()+1];
        for(int i = triangle.size()-1; i >= 0; i--){
            if(i == triangle.size()-1){
                for(int j = 0; j < triangle.get(i).size(); j++){
                    dp[j] = triangle.get(i).get(j);
                }
            }
            else{
                for(int j = 0; j < triangle.get(i).size(); j++){
                    dp[j] = Math.min(dp[j],dp[j+1]) + triangle.get(i).get(j);
                }
            }
        }
        
        return dp[0];
    }
```

### 参考资料
https://youtu.be/p1LlPZYw42g