https://leetcode.com/problems/permutation-sequence/

## 解题思路
1. 排列的题，本题的思路很巧妙，想得到就很简单
2. 题目的思路从前面的位开始逐个判断是哪个数字
3. 首先排除第一个数字之外的数字有几种组合方式，通过k除以刚才的组合数，就能得到第一个数字(从0开始)
4. 所以我们需要得到每个数字能组成的组合大小，存放在fact数组里
5. 然后通过k/fact[i]来判断，nums中的具体数字，加入到Stringbuilder之中即可
## 代码
```java
	public String getPermutation(int n, int k) {
        List<Integer> nums = new ArrayList<>();
        for(int i = 1; i <= n; i++){
            nums.add(i);
        }
        
        int[] fact = new int[n];
        fact[0] = 1;
        for(int i = 1; i < n; i++){
            fact[i] = fact[i-1] * i;
        }
        
        k--;
        StringBuilder sb = new StringBuilder();
        for(int i = n-1; i >= 0; i--){
            int num = nums.remove(k / fact[i]);
            sb.append(num);
            k %= fact[i];
        }
        
        return sb.toString();
    }
```
## 参考
https://youtu.be/MyiYm_xqbu8