# Summary Ranges
#每日技术

### 题目
You are given a sorted unique integer array nums.
Return the smallest sorted list of ranges that cover all the numbers in the array exactly. That is, each element of nums is covered by exactly one of the ranges, and there is no integer x such that x is in one of the ranges but not in nums

### 解题思路
遍历数组，先记录左边位置的值，如果元素连续则将指针i一直往后移动直到元素断开位置，然后将left->nums[i]记录到string的list之中

如果是单个元素则直接存入list之中

### 代码
```java
	public List<String> summaryRanges(int[] nums) {
        List<String> result = new ArrayList<>();
        if(nums == null || nums.length == 0){ return result; }
        
        for(int i = 0; i < nums.length; i++){
            int left = nums[i];
            while(i < nums.length - 1 && nums[i] + 1 == nums[i+1]){
                i++;
            }
            
            if(left != nums[i]){
                result.add(left + "->" + nums[i]);
            }
            else {
                result.add(left + "");
            }
        }
        
        return result;
    }
```

### 参考资料
https://youtu.be/CQC8rmyjAkg