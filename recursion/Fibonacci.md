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

## 2d array pattern

Ref: BOJ 1074

- 수식
``` python
N, r, c = map(int, input().split())

# Z: 0,0 기준으로 x, y 의 숫자
def Z(sz, x, y):
    if sz == 1:
        return 0
    sz //= 2
    for i in range(2):
        for j in range(2):
            if x < sz * (i+1) and y < sz * (j+1):
                return (i*2+j) * sz*sz + Z(sz, x-sz*i, y-sz*j)

print(Z(2**N, r, c))
```

- 비트와이즈 !
``` python
n, r, c = map(int, input().split())
s = 0
while n:
    n -= 1
    s += (r>>n<<1|c>>n)<<n+n
    r &= (1<<n)-1
    c &= (1<<n)-1
print(s)
```

- while (recursion 대체)
``` python
import sys
sys.setrecursionlimit(10000)
N, r, c = map(int, sys.stdin.readline().split())
ans = 0
i = 0
while(N):
    b = pow(2, N)//2
    if c < b and r < b: i = 0
    elif c >= b and r < b: i = 1
    elif c < b and r >= b: i = 2
    else: i = 3

    c %= b
    r %= b
    ans += pow(b,2)*i
    N -= 1

print(ans)
```

- recursion
``` python
import sys
sys.setrecursionlimit(10000)
N, r, c = map(int, sys.stdin.readline().split())
ans = 0
dx, dy = [0, 0, 1, 1], [0, 1, 0, 1]

def chk(x,y):
    global ans
    if x == c and y == r:
        print(ans)
        return
    ans += 1

def dfs(x, y, n):
    global ans
    if n == 2:
        for i in range(4):
            chk(x+dx[i], y+dy[i])
        return
    dfs(x, y, n // 2)
    dfs(x, y + n // 2, n // 2)
    dfs(x + n // 2, y, n // 2)
    dfs(x + n // 2, y + n // 2, n // 2)

dfs(0, 0, pow(2, N))
```

## Complete search

Ref: BOJ 7490

- recursion

    ``` python
    def zero(s, n):
        if n > N:
            if eval(s.replace(" ", "")) == 0:
                result.append(s)
        else:
            zero(f"{s}+{str(n)}", n + 1)
            zero(f"{s}-{str(n)}", n + 1)
            zero(f"{s} {str(n)}", n + 1)

    for _ in range(int(input())):
        N = int(input())
        result = []
        zero("1", 2)
        result.sort()
        print("\n".join(result))
        print()
    ```

- No recursion

    ``` python
    from itertools import product

    for _ in range(int(input())):
        n = int(input())
        ops = list(product(' +-', repeat = n - 1))
        num = ''.join([str(i+1) for i in range(n)])
        
        for i in range(len(ops)):
            temp = '1'
            for j in range(n - 1):
                temp += ops[i][j] + num[j + 1]
            if eval(temp.replace(" ", "")) == 0:
                print(temp)
        print()
    ```
