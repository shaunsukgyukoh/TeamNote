## Binary search

``` python
def binary_search(data, search):
    print (data)
    if len(data) == 1:
        return True if search == data[0] else False
    if len(data) == 0:
        return False
    
    mid = len(data) // 2
    if search == data[mid]:
        return True
    else:
        return binary_search(data[mid+1:], search) if search > data[mid] else binary_search(data[:mid], search)
```