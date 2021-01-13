## Fibonacci

Ref: BOJ 2747

- Recursion (easier)
    ``` python
    def fibo(n):
        return n if n < 2 else fibo(n-1)+fibo(n-2)
    
    print(fibo(int(input())))
    ```

- No recursion (faster)
    ``` python
    n = int(input())
    a, b = 1
    while n > 0:
        a,b = b, a+b
        n -= 1
    print(a)
    ```
