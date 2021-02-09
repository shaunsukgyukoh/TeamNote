## Longest Common Subsequence

Subsequence: String w/o continuity (apple: apl)
vs  
Substring: Continuous string (apple: ppl)

``` python
# pseudo code

if i == 0 or j == 0:
    LCS[i][j] = 0 
elif str1 == str2:
    LCS[i][j] = LCS[i-1][j-1] + 1
else:
    LCS[i][j] = max(LCS[i][j-1], LCS[i-1][j])
```

### Levenshtein Dist. / Edit Dist. algo.

``` python
# pseudo code

dp = [[0]*(len(str2)+1) for _ in range(len(str1)+1)]
for i in range(1, len(str1)+1): dp[i][0] = i
for j in range(1, len(str2)+1): dp[0][j] = j

# let len(str1) <= len(str2)
for i in (1, len(str1)):
    for j in (1, len(str2)):
        dp[i][j] = dp[i-1][j-1] if str1 == str2 else 1 + min(dp[i][j-1], dp[i-1][j], dp[i-1][j-1])
```
