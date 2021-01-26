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

``` cpp
#include <bits/stdc++.h>

using namespace std;

int n = 5;
int data[n] = {0, 1, 2, 3, 4};

int main(void){
    for (int i = 1; i < n; i++){
        for (int j = i; j > 0; j--) {
            if (data[j] < data[j-1]){
                swap(data[j], data[j-1]);
            }
            else break;
        }
    }
    for (int i = 0; i < n ; i++) cout << data[i] << ' ';
    return 0;
}
```

``` java
import java.util.*;

public class Main {

    public static void main(String[] args) {
        int[] data = {0, 1, 2, 3, 4};
        int n = data.length
        
        for(int i = 1; i < n; i++) {
            for (int j = i; j > 0; j--) {
                if (data[j] < data[j-1]){
                    int temp = data[i];
                    data[i] = a[j-1];
                    data[j-1] = temp;
                }
                else break;
            }
        }
        for(int i = 0; i <  n; i++) {
            System.out.println(data[i] + " ");
        }
    }
}
```