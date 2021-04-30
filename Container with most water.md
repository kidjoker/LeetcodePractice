# Container with most water 
#每日技术

```java
class Solution {
    public int maxArea(int[] height) {
        int ans = 0;
        int left = 0;
        int right = height.length-1;
        
        while(left < right){
            int curArea = Math.min(height[left],height[right]) * (right - left);
            ans = Math.max(ans,curArea);
            
            if(height[left] < height[right]){
                left++;
            }
            else{
                right--;
            }
        }
        
        return ans;
    }
}
```

### 运用木桶原理的思想解题，提高木桶的水需要提高短板
使用双指针，初始化的时候分别指向数组的头和尾。同理，对于两面墙，我们需要向左或向右寻找更高的墙，然后看当前的面积是否大于ans(暂时的最大值)