## Palindrome

``` python
def palindrome(string):
    if len(string) <= 1:
        return True
    
    return palindrome(string[1:-1]) if string[0] == string[-1] else False
```