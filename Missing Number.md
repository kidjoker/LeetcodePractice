# Missing Number
#每日技术

### 题目
Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array.
Follow up: Could you implement a solution using only O(1) extra space complexity and O(n) runtime complexity?

### 解题思路
	1. 排序之后，元素一定是连续的，如果出现跳跃的情况，那么跳开的数字就是缺失的元素
	2. 假设是1，n的连续数组没有确实元素，得到一个和；将数组中的所有元素求和，因为只确实一个元素，两者相减就是缺失的元素
	3. 将1，n的元素与数组的元素分别异或，因为相同元素异或位0，所以只剩一个缺失的元素是落单的，所以最终得到的结果就是缺失元素
### 代码
```java
	//排序法
	public int missingNumber(int[] nums) {
        Arrays.sort(nums);
        
        for(int i = 0; i < nums.length-1; i++){
            if(nums[i+1] - nums[i] > 1){
                return nums[i] + 1;
            }
        }
        return nums[0] == 0 ? nums.length : 0;
    }

	//加总求和法
	public int missingNumber(int[] nums) {
        int n = nums.length;
        int sum = 0;
        for(int i = 0; i < nums.length; i++){
            sum += nums[i];
        }
        
        return n*(n+1)/2 - sum;
    }

	//XOR法
	public int missingNumber(int[] nums) {
        int x = 0;
        for(int i = 0; i < nums.length; i++){
             x = x ^ i ^ nums[i];
        }
        x = x ^ nums.length;
        return x;
    }
```

### 参考资料
https://youtu.be/Dq0jQX3YNKg