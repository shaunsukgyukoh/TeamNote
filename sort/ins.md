## Insertion sort

``` python
def insertion_sort(data):
    for i in range(len(data) - 1):
        for ii in range(i + 1, 0, -1):
            if data[ii] < data[ii - 1]:
                data[ii], data[ii - 1] = data[ii - 1], data[ii]
            else: break
    return data
```
