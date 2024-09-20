# Interleaving-String

This solution determines if a given string s3 is formed by interleaving two other strings, s1 and s2. An interleaving is a configuration where s1 and s2 are divided into multiple substrings, and their concatenation follows an alternating pattern. The task is to check whether s3 can be created by merging the characters of s1 and s2 in such an interleaved manner, ensuring that the relative order of characters in both s1 and s2 is preserved.
Example:
For s1 = "abc", s2 = "def", and s3 = "adbcef", the function should return True, as s3 is an interleaving of s1 and s2.
Approach:
Use dynamic programming to check whether s3 can be formed by interleaving the substrings of s1 and s2 while maintaining their respective orders.

class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        m, n, l = len(s1), len(s2), len(s3)
        if m + n != l:
            return False
        
        if m < n:
            return self.isInterleave(s2, s1, s3)
        
        dp = [False] * (n + 1)
        dp[0] = True
        
        for j in range(1, n + 1):
            dp[j] = dp[j-1] and s2[j-1] == s3[j-1]
        
        for i in range(1, m + 1):
            dp[0] = dp[0] and s1[i-1] == s3[i-1]
            for j in range(1, n + 1):
                dp[j] = (dp[j] and s1[i-1] == s3[i+j-1]) or (dp[j-1] and s2[j-1] == s3[i+j-1])
        
        return dp[n]
