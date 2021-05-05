# Trapping rain water
#每日技术

```java
	public int trap(int[] height) {
        int result = 0;
        
        int maxHeightIndex = 0;
        int curMax = 0;
        for(int i = 0; i < height.length; i++){
            if(height[i] > curMax){ 
                curMax = height[i];
                maxHeightIndex = i;
            }
        }
        
        int leftMost = 0;
        for(int i = 0; i < maxHeightIndex; i++){
            if(height[i] > leftMost){
                leftMost = height[i];
            }
            if(height[i] < leftMost){
                result += (leftMost - height[i]);
            }
        }
        
        int rightMost = 0;
        for(int i = height.length - 1; i >maxHeightIndex; i--){
            if(height[i] > rightMost){
                rightMost = height[i];
            }
            if(height[i] < rightMost){
                result += (rightMost - height[i]);
            }
        }
        
        return result;
    }
```

### 找到中间的最高桶位，从两边依此向中间推进
1. 先找到最高位
2. 从左边向最高位靠近，记录左半边的最高位，比最高位高则更新，低说明可以储水
3. 从右边向最高位靠近，记录右半边的最高位，比最高位高则更新，低说明可以储水