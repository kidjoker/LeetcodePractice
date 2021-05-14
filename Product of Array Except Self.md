# Product of Array Except Self
#每日技术

### 题目
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].
The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
You must write an algorithm that runs in O(n) time and without using the division operation.

### 解题思路
	1. 累乘是由左半边和右半边组成的，所以解题思路就是先刷一遍数组得到左半边的积，因为前后两个积之间有公式关系
	2. 然后计算右半边，同理也可以由递推公式得到

### 代码
```java
	public int[] productExceptSelf(int[] nums) {
        int[] res = new int[nums.length];
        
        for(int i = 0; i < nums.length; i++){
            if(i == 0){ res[i] = 1; }
            else{ res[i] = res[i-1] * nums[i-1]; }
        }
        
        int right = 1;
        for(int i = nums.length-1; i >= 0; i--){
            res[i] = res[i] * right;
            right *= nums[i];
        }
        
        return res;
    }
```

### 参考资料
https://youtu.be/rpQhKorJRd8