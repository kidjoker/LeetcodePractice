# Find Minimum in Rotated Sorted Array
#每日技术

### 题目
Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:
	* 	[4,5,6,7,0,1,2] if it was rotated 4 times.
	* 	[0,1,2,4,5,6,7] if it was rotated 7 times.
Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].
Given the sorted rotated array nums of unique elements, return the minimum element of this array.
You must write an algorithm that runs in O(log n) time.

### 解题思路
	1. 数组对应O(logN)的复杂度，应该联想到分治的思想，对半组成树的形式就是logN
	2. 题目是求整个数组的最小值，分解成左半边的最小值和右半边的最小值进行比较，通过递归的方式得到最终的最小值
	3. 当nums[left]<nums[right]说明当前这一半的数组已经是有序的，直接返回nums[left]
	4. 当数组只有一个或两个元素的时候就不用继续向下递归直接求的结果即可

### 代码
```java
	public int findMin(int[] nums) {
        return findMin(nums,0,nums.length-1);   
    }
    
    private int findMin(int[] nums, int left, int right){
        if(left + 1 >= right){return Math.min(nums[left],nums[right]);}
        if(nums[left] < nums[right]){return nums[left];}
        
        int mid = left + (right-left)/2;
        return Math.min(findMin(nums,left,mid),findMin(nums,mid+1,right));
    }
```

### 参考资料
https://youtu.be/P4r7mF1Jd50