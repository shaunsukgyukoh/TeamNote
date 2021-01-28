## Prefix sum

- Get partial sum for sequence in given range
- O(N + M)

prefixSum -> P[R] - P[L-1]

|| |10|20|30|40|50|
|-|-|-|-|-|-|-|  
|prefix sum|0|10|30|60|100|150|

``` python
n = 5
data = [10, 20, 30, 40, 50]

# calculate prefix sum array
sumNum = 0
prefix_sum = [0]
for i in data:
    sumNum += i
    prefix_sum.append(sumNum)

# get sum in range
left = 3
right = 4
print(prefixSum[right] - prefix_sum[left-1])
```