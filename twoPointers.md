## Two pointers

- Finding # of partial sequence w/ certain sum value
- O(N)

``` python
n, m = 5, 5 # get data length n, partial sum m
data = [1, 2, 3, 2, 5]

result = sumNum = end = 0

for start in range(n): # increase start 
    while sumNum < m and end < n: # move end as far as possible
        sumNum += data[end]
        end += 1
    if sumNum == m: # Add when partial sum == m
        result += 1
    sumNum -= data[start]

print(result)
```