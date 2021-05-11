# Find the Duplicate Number
#每日技术

### 题目
Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.
There is only one repeated number in nums, return this repeated number

### 解题思路
	1. 二分法
		1. 如果小于等于当前数字的个数小于当前数字，表示在这个数字之前没有重复，我们需要在后面的数字范围里寻找可能值
		2. 否则说明在这个数字之前存在重复，暂且设定ans为当前数字，因为当前数字可能就是唯一重复的元素（因为只存在一个重复的数字，所以需要寻找满足条件的最小值）
			1. 然后不断向前或者向后，找到最后重复的元素
	2. 快慢指针
		1. 我们将当前元素定义为下一个元素的index，这样就能串联出一个链表，因为有重复元素的存在，所以链表存在回环
		2. 所以我们使用快慢指针判断出回环相遇的位置

### 代码
```java
	//二分法
	public int findDuplicate(int[] nums) {
        int left = 1, right = nums.length - 1;
        int mid = 0, ans = -1;
        while(left <= right){
            mid = left + (right - left)/2;
            int count = 0;
            for(int i = 0; i < nums.length; i++){
                if(nums[i] <= mid){ count++; }
            }
            if(count <= mid){
                left = mid + 1;
            }
            else {
                ans = mid;
                right = mid -1;
            }
        }
        
        return ans;
    }

	//快慢指针
	public int findDuplicate(int[] nums) {
        int slow = nums[nums[0]], fast = nums[slow];
        while(slow != fast){
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        slow = nums[0];
        while(slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        
        return fast;
    }
```

### 参考资料
https://youtu.be/u_gg0uVZdsE