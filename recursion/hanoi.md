## Hanoi

``` python
def TowerOfHanoi(n , src, dest, target): 
    if n == 1: 
        print(src," -> ",dest)
        return
    TowerOfHanoi(n-1, src, target, dest) 
    print("Move disk",n,"from ",src," -> ",dest) 
    TowerOfHanoi(n-1, target, dest, src) 
```
