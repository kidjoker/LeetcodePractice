https://leetcode.com/problems/expression-add-operators/

## 解题思路
1. 首先这是一道dfs的题目，先搭好框架
	1. result
	2. case
	3. dfs
	4. return
		1. dfs
			1. 退出条件
			2. 拆分dfs
2. 在拆分dfs的时候，如果这是第一个数字，那不需要改变path直接拼接即可
3. 否则需要通过三次dfs，分别走+，-，*
4. 其中*的时候，因为优先级的问题，需要把上一次dfs+的数字减去，然后和现在的cur相乘，再加上去，所以需要保存每次调用dfs，需要previous(当前的cur就是dfs后的prev)
5. 其中06这样的数字是不合理的，需要剔除

## 代码
```java
	public List<String> addOperators(String num, int target) {
        List<String> result = new ArrayList<>();
        if(num == null || num.length() == 0){ return result; }
        
        dfs(result, num, 0, "", 0, target, 0);
        return result;
    }
    
    private void dfs(List<String> result, String num, int pos, String path, long count, int target, long prev){
        if(pos == num.length()){
            if(count == target){ result.add(path); }
            return;
        }
        
        for(int i = pos; i < num.length(); i++){
            if(i != pos && num.charAt(pos) == '0'){ break; }
            long cur = Long.parseLong(num.substring(pos,i+1));
            if(pos == 0){
                dfs(result,num,i+1, path+cur,cur,target,cur);
            }
            else{
                dfs(result,num,i+1,path+"+"+cur,count+cur,target,cur);
                dfs(result,num,i+1,path+"-"+cur,count-cur,target,-cur);
                dfs(result,num,i+1,path+"*"+cur,count-prev + (prev*cur),target,cur*prev);
            }
        }
    }
```

## 参考
https://youtu.be/AXNb-stFNb4