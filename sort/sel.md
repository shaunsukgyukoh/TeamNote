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

``` cpp
#include <bits/stdc++.h>

using namespace std;

int n = 5;
int data[n] = {0, 1, 2, 3, 4};

int main(void){
    for (int i = 0; i < n; i++){
        int lowest = i;
        for (int j = i + 1; j < n; j++) {
            if (data[loweset] > data[j]){
                lowest = j;
            }
        }
        swap(data[i]. data[lowest]);
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
        
        for(int i = 0; i < n; i++) {
            int lowest = i;
            for(int j = i + 1; j < n; j++) {
                if (data[lowest] > data[j]) {
                    lowest = j;
                }
            }
            int temp = data[i];
            data[i] = a[lowest];
            data[lowest] = temp;
        }
        for(int i = 0; i <  n; i++) {
            System.out.println(data[i] + " ");
        }
    }
}
```