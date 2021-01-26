## Quck sort

``` python
def qsort(data):
    if len(data) <= 1:
        return data
    
    pivot = data[0]
    left = [ item for item in data[1:] if pivot > item ]
    right = [ item for item in data[1:] if pivot <= item ]
    
    return qsort(left) + [pivot] + qsort(right)
```

``` cpp
#include <bits/stdc++.h>

using namespace std;

int n = 5;
int data[n] = {0, 1, 2, 3, 4};

void quickSort(int* data, int start, int end){
    
    if (start >= end) return;
    int pivot = start;
    int left = start + 1;
    int right = end;
    while (left <= right){
        while (left <= end && data[left] <= data[pivot]) left++;
        while (right > start && data[right] >= data[pivot]) right--;
        if (left > right) swap(data[pivot], data[right]);
        else swap(data[left], data[right]);
    }
    quickSort(data, start, right - 1);
    quickSort(data, right + 1, end);
}

int main(void){
    quickSort(data, 0, n-1);
    for (int i = 0; i < n ; i++) cout << data[i] << ' ';
    return 0;
}
```

``` java
import java.util.*;

public class Main {

    public static void quickSort(int[] data, int start, int end) {
        if (start >= end) return;
        int pivot = start;
        int left = start + 1;
        int right = end;
        while (left <= right){
            while (left <= end && data[left] <= data[pivot]) left++;
            while (right > start && data[right] >= data[pivot]) right--;
            if (left > right) {
                int temp = data[pivot];
                data[pivot] = data[right];
                data[right] = temp;
            } else {
                int temp = data[left];
                data[left] = data[right];
                data[right] = temp;
            }
        }
        quickSort(data, start, right - 1);
        quickSort(data, right + 1, end);
    }
    
    public static void main(String[] args) {
        int n = 5;
        int[] data = {1, 3, 2, 5, 4};

        quickSort(data, 0, n-1);
        for(int i = 0; i <  n; i++) {
            System.out.println(data[i] + " ");
        }
    }

}
```