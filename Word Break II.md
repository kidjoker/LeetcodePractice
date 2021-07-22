https://leetcode.com/problems/word-break-ii/

## 解题思路
1. 动态规划+Memory
2. 思想就是从前开始遍历，如果出现一个word在dict里，就进行切分，然后将右半部分递归调用
3. Set是为了对dict去重
4. dfs函数的返回表达就是对当前s的所有可能的sentence
5. 所以当我们将右半部分递归调用dfs的时候，就需要遍历递归返回的结果集，将left拼接里面的每个result，然后将其放入到本层结果集里
6. 使用HashMap记录所有字段对应的拆分结果，避免不必要的操作
7. 因为可能存在AB,A,B的dict，所以在拆分s之前，、判断s是否已经在dict里，先将其放入结果集里

## 代码
```java
	private Map<String,List<String>> memory = new HashMap<>();
     
    public List<String> wordBreak(String s, List<String> wordDict) {
        if(s == null || s.length() == 0){ return null; }
        
        Set<String> set = new HashSet<>();
        for(String word : wordDict){
            set.add(word);
        }
        
        return dfs(s, set);
    }
    
    private List<String> dfs(String s, Set<String> set){
        if(memory.containsKey(s)){ return memory.get(s); }
        
        List<String> list = new ArrayList<>();
        if(set.contains(s)){ list.add(s); }
        
        for(int i = 0; i < s.length(); i++){
            String left = s.substring(0, i+1);
            if(!set.contains(left)){ continue; }
            
            List<String> rights = dfs(s.substring(i+1, s.length()), set);
            for(String ss : rights){
                list.add(left + " " + ss);
            }
        }
        
        return list;
    }
```

## 参考
https://zxi.mytechroad.com/blog/leetcode/leetcode-140-word-break-ii/