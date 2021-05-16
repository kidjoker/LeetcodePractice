# Two Sum II - Input array is sorted
#每日技术

### 题目
Given an array of integers numbers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.
Return the indices of the two numbers (1-indexed) as an integer array answer of size 2, where 1 <= answer[0] < answer[1] <= numbers.length.
You may assume that each input would have exactly one solution and you may not use the same element twice

### 解题思路
	1. 将两个指针分别指向最左边和最右边，向中间递进
	2. 如果sum小于target则增加left，否则减小right
	3. 直到sum等于target，按照base 1的形式返回数据下标

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