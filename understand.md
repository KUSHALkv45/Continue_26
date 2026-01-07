```cpp
  class Solution {
public:
    int solve(int i, int n, int prev1, int prev2, int prev3, int mod,
              vector<vector<vector<vector<int>>>>& dp) {
        if (i == n) {
            return 1;
        }
        if (dp[i][prev1][prev2][prev3] != -1) {
            return dp[i][prev1][prev2][prev3];
        }
        int ans = 0;
        for (int col1 = 1; col1 <= 3; col1++) {
            if (col1 == prev1) {
                continue;
            }
            for (int col2 = 1; col2 <= 3; col2++) {
                if (col2 == prev2 || col2 == col1) {
                    continue;
                }
                for (int col3 = 1; col3 <= 3; col3++) {
                    if (col3 == prev3 || col3 == col2) {
                        continue;
                    }
                    ans = (ans + solve(i + 1, n, col1, col2, col3, mod, dp)) %
                          mod;
                }
            }
        }
        return dp[i][prev1][prev2][prev3] = ans;
    }
    int numOfWays(int n) {
        int mod = 1e9 + 7;
        vector<vector<vector<vector<int>>>> dp(
            n, vector<vector<vector<int>>>(
                   4, vector<vector<int>>(4, vector<int>(4, -1))));

        return solve(0, n, 0, 0, 0, mod, dp);
    }
};
```
```java
  // Understand this code's TC 07-01-26 wrote it but I want to understand it properly TC  LEETCODE 1340
  class Solution {
    public int maxJumps(int[] nums, int d) {
        int n = nums.length;
        int [] memo = new int [n];

        // Arrays.fill(memo,-1);
        int ans = 0;
        for(int i = 0 ; i < n ; i++){
            if(memo[i] == 0){
                ans = Math.max(ans,find(d,nums,i,memo)) ;
            }
        }

        return ans;
    }
    private int find(int d , int [] nums , int idx , int [] memo){
        if(memo[idx] != 0){
            return memo[idx];
        }
        int ans = 1;

        // right
        for(int i = idx+1 ; i <= Math.min(idx+d,nums.length-1) ; i++){
            if(nums[i] >= nums[idx]){
                break;
            }
            else{
                ans = Math.max(ans,1+find(d,nums,i,memo));
            }
        }

        // left
        for(int i = idx-1 ; i >= Math.max(0,idx-d) ; i--){
            if(nums[i] >= nums[idx]){
                break;
            }
            else{
                ans = Math.max(ans,1+find(d,nums,i,memo));
            }
        }

        memo[idx] = ans;

        return ans;
    }

}
```
