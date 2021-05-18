# Minimum Size Subarray Sum
#每日技术

### 题目
Given an array of positive integers nums and a positive integer target, return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

### 解题思路
	1. 双指针，滑动窗口的思想
	2. 使用两个指针来确定一个窗口，当right向右增大窗口找到第一个sum大于等于target的情况，因为是右边递增的，所有如果右边的值很大而左边的值很小，则删除左边的元素可以缩小窗口
	3. 当删除左边元素直到sum小于target，说明窗口太小了，重新向右增大窗口
	4. 这样遍历整个数组就能得到最小窗口
### 代码
```java
	public int minSubArrayLen(int target, int[] nums) {
        int left = 0;
        int sum = 0;
        int result = Integer.MAX_VALUE;
        
        for(int right = 0; right < nums.length; right++){
            sum += nums[right];
            while(sum >= target){
                result = Math.min(result,right-left+1);
                sum -= nums[left];
                left++;
            }
        }
        
        return result == Integer.MAX_VALUE ? 0 : result;
    }
```

### 参考资料
https://youtu.be/jp15K7dTCHc