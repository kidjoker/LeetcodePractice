# Intersection of Two Arrays II
#每日技术

### 题目
![](Intersection%20of%20Two%20Arrays%20II/%E7%85%A7%E7%89%87%202021%E5%B9%B46%E6%9C%887%E6%97%A5%20%E4%B8%8B%E5%8D%8873352.jpg)

### 解题思路
	1. HashMap
		1. 统计数组元素出现的次数放在hashmap中
		2. 遍历另一个数组，如果在hashmap中出现过，则放到result中，并且hashmap对应的value减一
	2. 双指针
		1. 对两个数组进行排序
		2. 找到数组中相等的元素输入到set中
		3. 因为已经排好序，不相等的时候我们只需要移动一个指针就好了
		4. 然后遍历set输入到int[]中
### 代码
```java
	//HashMap
	public int[] intersect(int[] nums1, int[] nums2) {
		   Map<Integer,Integer> map = new HashMap<>();
        for(int num : nums1){
            if(map.get(num) == null){
                map.put(num,1);
            }
            else{    
                map.put(num,map.get(num)+1);
            }
        }
        
        List<Integer> list = new ArrayList<>();
        for(int num : nums2){
            if(map.get(num) != null && map.get(num) > 0){
                list.add(num);
                map.put(num,map.get(num)-1);
            }
        }
        
        int[] array = new int[list.size()];
        int i = 0;
        for(Integer num : list){
            array[i++] = num;
        }
        
        return array;
	}

  //two pointer
	public int[] intersect(int[] nums1, int[] nums2) {
        int i = 0, j = 0;
        List<Integer> list = new ArrayList<>();
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        
        while(i < nums1.length && j < nums2.length){
            if(nums1[i] == nums2[j]){
                list.add(nums1[i]);
                i++;
                j++;
            }
            else if(nums1[i] < nums2[j]){
                i++;
            }
            else{
                j++;
            }
        }
        
        int[] array = new int[list.size()];
        i = 0;
        for(Integer num : list){
            array[i++] = num;
        }
        
        return array;
	}
```

### 参考资料
https://youtu.be/1CjkFzpkfJg