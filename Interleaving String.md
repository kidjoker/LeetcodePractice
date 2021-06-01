# Interleaving String
#每日技术

### 题目
Given strings s1, s2, and s3, find whether s3 is formed by an interleaving of s1 and s2.
An interleaving of two strings s and t is a configuration where they are divided into non-empty substrings such that:
	* 	s = s1 + s2 + ... + sn
	* 	t = t1 + t2 + ... + tm
	* 	|n - m| <= 1
	* 	The interleaving is s1 + t1 + s2 + t2 + s3 + t3 + ... or t1 + s1 + t2 + s2 + t3 + s3 + ...
Note: a + b is the concatenation of strings a and b

### 解题思路
	1. 字符串的题目可能都是DP问题
	2. 看到两个String的情况，联想到2D dp的解决方案
	3. 2D就是走路法 ![](Interleaving%20String/%E7%85%A7%E7%89%87%202021%E5%B9%B46%E6%9C%881%E6%97%A5%20%E4%B8%8B%E5%8D%88113921.jpg)
	* 通过不断向下或者向右的方式，如果能走到右下角即为成功
	* 想要达到黄色的点，先判断能否走到S1和Ｓ2，然后看S1和S2是否能够走向黄点
	* 对于本题就变成dp[i-1][j]或dp[i][j-1]是否为true，然后s1或s2后续的点与s3后续的点是否相等，找到了递推公式	
### 代码
```java
	public boolean isInterleave(String s1, String s2, String s3) {
        int s1Length = s1.length();
        int s2Length = s2.length();
        int s3Length = s3.length();
        
        if(s1Length + s2Length != s3Length){ return false; }
        
        boolean[][] dp = new boolean[s1Length+1][s2Length+1];
        dp[0][0] = true;
        
        for(int i = 0; i < s1Length+1; i++){
            for(int j = 0; j < s2Length+1; j++){
                if(i == 0 && j > 0){
                    dp[i][j] = dp[i][j-1] & (s2.charAt(j-1) == s3.charAt(j-1));
                }
                if(i > 0 && j == 0){
                    dp[i][j] = dp[i-1][j] & (s1.charAt(i-1) == s3.charAt(i-1));
                }
                if(i > 0 && j > 0){
                    dp[i][j] = (dp[i][j-1] & (s2.charAt(j-1) == s3.charAt(i+j-1))) |
                                (dp[i-1][j] & (s1.charAt(i-1) == s3.charAt(i+j-1)));
                }
            }
        }
        
        return dp[s1Length][s2Length];
    }
```

### 参考资料
https://blog.csdn.net/m0_37683327/article/details/103926883