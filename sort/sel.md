## Selection sort

``` python
def selection_sort(data):
    for i in range(len(data) - 1):
        lowest = i
        for index in range(i + 1, len(data)):
            if data[lowest] > data[index]:
                lowest = index
        data[lowest], data[i] = data[i], data[lowest]
    return data
```