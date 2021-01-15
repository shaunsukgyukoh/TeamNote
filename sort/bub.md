## Bubble sort

``` python
def bubblesort(data):
    for i in range(len(data) - 1):
        swap = False
        for ii in range(len(data) - i - 1):
            if data[ii] > data[ii + 1]:
                data[ii], data[ii + 1] = data[ii + 1], data[ii]
                swap = True
        
        if swap == False: break
    return data
```
