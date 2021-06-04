# Intersection of Two Arrays
#每日技术

### 题目
![](Intersection%20of%20Two%20Arrays/%E7%85%A7%E7%89%87%202021%E5%B9%B46%E6%9C%884%E6%97%A5%20%E4%B8%8B%E5%8D%8855058.jpg)

### 解题思路
	1. 二叉树搜索
		1. 使用二叉搜索树，先要对进行搜索的数组nums1进行排序
		2. 遍历nums2，看在nums1中是否出现，出现则保存在set中(因为有set来保证唯一性)
		3. 然后遍历set输入到int[]中
	2. 双指针
		1. 对两个数组进行排序
		2. 找到数组中相等的元素输入到set中
		3. 因为已经排好序，不相等的时候我们只需要移动一个指针就好了
		4. 然后遍历set输入到int[]中
### 代码
```java
	//binary search
	public int[] intersection(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        
        Set<Integer> intersectionSet = new HashSet<>();
        for(int i = 0; i < nums2.length; i++){
            if(find(nums2[i],nums1)){
                intersectionSet.add(nums2[i]);   
            }
        }
        
        int[] result = new int[intersectionSet.size()];
        int i = 0;
        for(int num : intersectionSet){
            result[i++] = num;
        }
        
        return result;
    }
    
    private boolean find(int target, int[] arr){
        int low = 0;
        int high = arr.length-1;
        
        while(low <= high){
            int mid = low + (high - low)/2;
            if(arr[mid] < target){
                low = mid + 1;
            }
            else if(arr[mid] > target){
                high = mid -1;
            }
            else {
                return true;
            }
        }
        
        return false;
    }

    //two pointer
	  public int[] intersection(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        
        int i = 0,j = 0;
        Set<Integer> intersectionSet = new HashSet<>();
        while(i < nums1.length && j < nums2.length){
            if(nums1[i] == nums2[j]){
                intersectionSet.add(nums1[i]);
                i++;
                j++;
            }
            else if (nums1[i] < nums2[j]){
                i++;
            }
            else{
                j++;
            }
        }
        
        int[] result = new int[intersectionSet.size()];
        i = 0;
        for(int num : intersectionSet){
            result[i++] = num;
        }
        
        return result;
    }
```

### 参考资料
https://youtu.be/XxStWmfXJRs