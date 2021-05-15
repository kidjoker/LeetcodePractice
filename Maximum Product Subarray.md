# Maximum Product Subarray
#每日技术

### 题目
Given an integer array nums, find a contiguous non-empty subarray within the array that has the largest product, and return the product.
It is guaranteed that the answer will fit in a 32-bit integer.
A subarray is a contiguous subsequence of the array.

### 解题思路
使用maxCurrent和minCurrent来标记当前可能的最大值和最小值
类似DP的思想，因为当前的值和前面的值是有关联的

### 代码
```java
	public int maxProduct(int[] nums) {
        int maxCur = nums[0], minCur = nums[0], max = nums[0];
        
        for(int i = 1; i < nums.length; i++){
            int nextMaxCur = maxCur*nums[i];
            int nextMinCur = minCur*nums[i];
            maxCur = Math.max(Math.max(nextMaxCur,nextMinCur),nums[i]);
            minCur = Math.min(Math.min(nextMaxCur,nextMinCur),nums[i]);
            max = Math.max(max,maxCur);
        }
        
        return max;
    }
```

### 参考资料
https://youtu.be/AtzfZHb35YI