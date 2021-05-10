# Increasing Triplet Subsequence
#每日技术

### 原题
Given an integer array nums, return true if there exists a triple of indices (i, j, k) such that i < j < k and nums[i] < nums[j] < nums[k]. If no such indices exists, return false

### 解题思路
贪心算法：获取当前遍历元素中最小的两个元素，只要有元素大于这两个元素就成立，但两个最小元素的位置需要分类讨论一下
情况一：min1的index小于min2的index，那最好就是符合条件的
情况二：min1的index大于min2的index，那么现在的min2一定是替换了原			先的min2，而发生替换之前的min1的index一定小于现在min2，			再配合现在的max，就是符合条件的

### 代码
```java
	public boolean increasingTriplet(int[] nums) {
        int min1 = Integer.MAX_VALUE;
        int min2 = Integer.MAX_VALUE;
        
        for(int num : nums){
            if(num < min1){ min1 = num; }
            else if(num > min1 && num < min2){ min2 = num; }
            else if(num > min2) { return true; }
        }
        
        return false;
    }
```

### 参考资料
https://youtu.be/xV_AS08-OeA