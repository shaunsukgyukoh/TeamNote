## Counting sort

- Use only if data is __integer__  and size is limited
  - If data is big and have small size (e.g. [0, 999999]), memory will be wasted a lot.
  - Effective when there's a lot of duplicate #s. (e.g. test scores)
- If data_size == N && max_val == K  -> _O_(__N + K__)

``` python
arr = [5, 3, 2, 1, 0]

cnt = [0] * (max(arr) + 1)

for i in range(len(arr)):
    cnt[arr[i]] += 1

for i in range(len(cnt)):
    for j in range(cnt[i]):
        print(i, end = ' ')
```

``` cpp
#include <bits/stdc++.h>
MAX_VALUE = 5

using namespace std;

int n = 5;
int arr[n] = {5, 3, 2, 1, 0};
int cnt[MAX_VALUE + 1];

int main(void){
    for (int i = 0; i < n; i++) cnt[arr[i]] += 1;
    for (int i = 0; i <= MAX_VALUE; i++){
        for (int j = 0; j < cnt[i]; j++){
            cout << i << ' ';
        }
    }
}
```

``` java
import java.util.*;

public class Main {
    public static final int MAX_VALUE = 9;

    public static void main(String[] args){
        int n = 5;
        int[] arr = {5, 2, 3, 1, 0};
        int[] cnt = new int[MAX_VALUE + 1];

        for (int i = 0; i < n; i++){
            cnt[arr[i]] += 1;
        }
        for (int i = 0; i <= MAX_VALUE; i++){
            for (int j = 0; j < cnt[i]; j++){
                System.out.print(i + " ");
            }
        }
    }
}
```