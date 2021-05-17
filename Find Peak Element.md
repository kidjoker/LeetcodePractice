# Find Peak Element
#每日技术

### 题目
A peak element is an element that is strictly greater than its neighbors.
Given an integer array nums, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks.
You may imagine that nums[-1] = nums[n] = -∞.
You must write an algorithm that runs in O(log n) time

### 解题思路
	1. 分治法
		1. 数组对应O(logN)的复杂度，应该联想到分治的思想，对半组成树的形式就是logN
		2. 题目是求整个数组的最小值，分解成左半边的最小值和右半边的最小值进行比较，通过递归的方式得到最终的最小值
		3. 当nums[left]<nums[right]说明当前这一半的数组已经是有序的，直接返回nums[left]
		4. 当数组只有一个或两个元素的时候不用继续向下递归直接求的结果即可
	2. mid
		1. 对于mid和mid+1的大小比较，来看当前是上升还是下降趋势来调整left和right的值
		2. 最后当left和right相邻的时候，就一定存在peak
### 代码
```java
	  //分治法
	  public int findPeakElement(int[] nums) {
        return findMax(nums,0,nums.length-1);
    }
    
    private int findMax(int[] nums, int left, int right){
        if(left + 1 >= right){
            return (nums[left] > nums[right]) ? left : right;
        }
        
        int mid = left + (right-left)/2;
        int leftMaxIndex = findMax(nums,left,mid);
        int rightMaxIndex = findMax(nums,mid+1,right);
        return (nums[leftMaxIndex] > nums[rightMaxIndex]) ? leftMaxIndex : rightMaxIndex;
    }

	//mid方法
	public int findPeakElement(int[] nums) {
        int left = 0;
        int right = nums.length-1;
        
        while(left + 1 < right){
            int mid = left + (right - left)/2;
            if(nums[mid] < nums[mid+1]){
                left = mid;
            }
            else{
                right = mid;
            }
        }
        
        if(nums[left] < nums[right]){
            return right;
        }
        else{
            return left;
        }
    }
```

### 参考资料
https://youtu.be/etuTPmks7Dc、