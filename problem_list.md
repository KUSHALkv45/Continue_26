```python

  ## LEETCODE : 1163 - 07-01-26  needed optimization as it acc my n^2 sol for now
  class Solution:
    def lastSubstring(self, s: str) -> str:
        
        di = {}

        maxi = ''

        n = len(s)

        for i in range(n-1,-1,-1):
            if s[i] in di and maxi == s[i]:
                if s[i:] > s[di[s[i]]:]:
                    di[s[i]] = i 
            if s[i] > maxi:
                maxi = s[i]
                di[s[i]] = i
        return s[di[maxi]:]©leetcode
```
