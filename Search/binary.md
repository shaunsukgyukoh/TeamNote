## Binary search

- Must be __sorted__
- O (log N)
- recommanded if data > 10,000,000 || searching range > 100,000,000,000
  - use `sys.stdin.readline().split().rstrip()`

Recursive:

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

``` python
# 이진 탐색 소스코드 구현 (재귀 함수)
def binary_search(array, target, start, end):
    if start > end:
        return None
    mid = (start + end) // 2
    # 찾은 경우 중간점 인덱스 반환
    if array[mid] == target:
        return mid
    # 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
    elif array[mid] > target:
        return binary_search(array, target, start, mid - 1)
    # 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
    else:
        return binary_search(array, target, mid + 1, end)
```

Iterative:

``` python
def binary_search(array, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        # If the target is found, return the mid index.
        if array[mid] == target:
            return mid
        # If the value of the mid index is greater than the target, search the left part.
        elif array[mid] > target:
            end = mid - 1
        # If the value of the mid index is smaller than the target, search the right part.
        else:
            start = mid + 1
    return None

n = 10
target = 13
array = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]

result = binary_search(array, target, 0, n - 1)
if result == None:
    print(None)
else:
    print(result + 1)
```

``` cpp
#include <bits/stdc++.h>

using namespace std;

// 이진 탐색 소스코드 구현(재귀 함수)
int binarySearch(vector<int>& arr, int target, int start, int end) {
    if (start > end) return -1;
    int mid = (start + end) / 2;
    // 찾은 경우 중간점 인덱스 반환
    if (arr[mid] == target) return mid;
    // 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
    else if (arr[mid] > target) return binarySearch(arr, target, start, mid - 1);
    // 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
    else return binarySearch(arr, target, mid + 1, end);
}

int n, target;
vector<int> arr;

int main(void) {
    // n(원소의 개수)와 target(찾고자 하는 값)을 입력받기 
    cin >> n >> target;
    // 전체 원소 입력받기 
    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;
        arr.push_back(x);
    }
    // 이진 탐색 수행 결과 출력 
    int result = binarySearch(arr, target, 0, n - 1);
    if (result == -1) {
        cout << "원소가 존재하지 않습니다." << '\n';
    }
    else {
        cout << result + 1 << '\n';
    }
}
```

``` java
import java.util.*;

public class Main {

    // 이진 탐색 소스코드 구현(재귀 함수)
    public static int binarySearch(int[] arr, int target, int start, int end) {
        if (start > end) return -1;
        int mid = (start + end) / 2;
        // 찾은 경우 중간점 인덱스 반환
        if (arr[mid] == target) return mid;
        // 중간점의 값보다 찾고자 하는 값이 작은 경우 왼쪽 확인
        else if (arr[mid] > target) return binarySearch(arr, target, start, mid - 1);
        // 중간점의 값보다 찾고자 하는 값이 큰 경우 오른쪽 확인
        else return binarySearch(arr, target, mid + 1, end);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // 원소의 개수(n)와 찾고자 하는 값(target)을 입력받기 
        int n = sc.nextInt();
        int target = sc.nextInt();

        // 전체 원소 입력받기 
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        // 이진 탐색 수행 결과 출력 
        int result = binarySearch(arr, target, 0, n - 1);
        if (result == -1) {
            System.out.println("원소가 존재하지 않습니다.");
        }
        else {
            System.out.println(result + 1);
        }
    }

}
```


### Parametric search

- 최적화 문제를 예/아니오 로 바꾸어 해결하는 기법
  - 예 ) 특정 조건을 만족하는 값을 탐색 범위를 좁혀가며 빠르게 찾는 최적화 문제
- 이진 탐색 활용

