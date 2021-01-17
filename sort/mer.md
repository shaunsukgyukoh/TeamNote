## Merge sort

Ref: BOJ 2751

``` python
def mergeSplit(data):
    if len(data) <= 1: return data
    mid = len(data) // 2
    l = mergeSplit(data[:mid])
    r = mergeSplit(data[mid:])
    return merge(l, r)

def merge(left, right):
    merged = []
    l_ptr, r_ptr = 0, 0

    
    while len(left) > l_ptr and len(right) > r_ptr:
    if left[l_ptr] > right[r_ptr]:
        merged.append(right[r_ptr])
        r_ptr += 1
    else:
        merged.append(left[l_ptr])
        l_ptr += 1

    if l_ptr >= len(left): merged += right[r_ptr:]
    else: merged += left[l_ptr:]
    return merged
```
