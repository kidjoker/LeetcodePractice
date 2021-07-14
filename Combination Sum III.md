https://leetcode.com/problems/combination-sum-iii/

## 解题思路
1. 套用backtrack的模版即可

## 代码
```java
	public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> result = new ArrayList<>();
        helper(result, new ArrayList<Integer>(), k, n, 1);
        return result;
    }
    
    private void helper(List<List<Integer>> result,List<Integer> list,int k, int n, int i){
        if(k == 0 && n == 0){
            result.add(new ArrayList(list));
            return;
        }
        for(;i < 10; i++){
            list.add(i);
            helper(result, list, k-1, n-i, i+1);
            list.remove(list.size()-1);
        }
    }
```

## 参考
https://youtu.be/qQcAm0CE21U