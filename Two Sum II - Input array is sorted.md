# Two Sum II - Input array is sorted
#每日技术

### 题目
Given an array of integers numbers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.
Return the indices of the two numbers (1-indexed) as an integer array answer of size 2, where 1 <= answer[0] < answer[1] <= numbers.length.
You may assume that each input would have exactly one solution and you may not use the same element twice

### 解题思路
使用maxCurrent和minCurrent来标记当前可能的最大值和最小值
类似DP的思想，因为当前的值和前面的值是有关联的

### 代码
```java
	public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length-1;
        
        while(left < right){
            int sum = numbers[left] + numbers[right];
            if(sum < target){
                left++;
            }
            else if(sum > target){
                right--;
            }
            else{
                return new int[]{left+1,right+1};
            }
        }
        
        return null;
    }
```

### 参考资料
https://youtu.be/iwkVVs6MuRo