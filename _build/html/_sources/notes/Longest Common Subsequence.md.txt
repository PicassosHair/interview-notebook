# Longest Common Subsequence

## Question List
516\. Longest Palindromic Subsequence \
583\. Delete Operation for Two Strings \
712\. Minimum ASCII Delete Sum for Two Strings \
718\. Maximum Length of Repeated Subarray \
1143\. Longest Common Subsequence


## Dynamic Programming Solution
For finding longest common subsequence, dynamic programming is the first solution coming to our mind. Leetcode 1143 is a typical example which 

### Leetcode 1143 <br>
#### Assume:
- `i` is the i-th char of text1
- `j` is the j-th char of text2 
- `dp` is a 2-dimension array `[(len(text1)+1)*(len(text2)+1)]`. `dp[j][i]` stores the length of longest Common Subsequece for `text1[:i]` and `text2[:j]`. 

#### Solution:
Calculate `dp[j][i]`
- `text1[i-1] == text2[j-1]`
**dp[j][i] = dp[j-1][i-1] + 1**
- `text1[i-1] != text2[j-1]`
**dp[j][i] = max(dp[j-1][i], dp[j][i-1])**: If (i-1)th char of text1 is not equal to (j-1)th char of text2, it will have the following 3 situations:
  - text1[i-2] == text2[j-1]: **dp[j][i] = dp[j][i-1]**
  - text1[i-1] == text2[j-2]: **dp[j][i] = dp[j-1][j]**
  - None of them is equal (It is included in the top 2 scenarios)

After calculating all values in `dp`, `dp[-1][-1]` will be the final result.

#### Graph:
![image](https://assets.leetcode.com/users/images/92c8aabd-fd52-4ac4-aa0c-8540d6b407bd_1604432372.6742601.png)

Green: Initial value 0 <br>
Yellow: Final Path

#### Code:
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:

        m, n = len(text1), len(text2)
		
		# Create 2-dimension array for storing the result
        dp = [[0] * (m + 1) for _ in range(n + 1)]

        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if text1[i - 1] == text2[j - 1]:
                    dp[j][i] = dp[j - 1][i - 1] + 1
                else:
                    dp[j][i] = max(dp[j - 1][i], dp[j][i - 1])

        return dp[-1][-1]

```