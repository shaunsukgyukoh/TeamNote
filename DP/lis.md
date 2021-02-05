## Longest Increasing Subsequence

for 0 <= j < i,  
D[i] = max(D[i], D[j] + 1) if arr[j] < arr[i]

``` python
# Using Binary search
from bisect import bisect_left as bl

def LIS(L):
    best = []
    for i in L:
        pos = bl(best, i)
        if len(best) <= pos: best.append(i)
        else: best[pos] = i
    return len(best)

n = int(input())
A = list(map(int,input().split()))[::-1] # reverse to make LIS
print(n - LIS(A))

# Regular
n = int(input())
arr = list(map(int, input().split()))
arr.reverse() # reverse to make LIS
dp = [1]*n

for i in range(1, n):
    for j in range(0, i):
        if arr[j] < arr[i]:
            dp[i] = max(dp[i], dp[j]+1)
print(n-max(dp))
```

``` cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	cin.tie(0), cout.tie(0);
	ios::sync_with_stdio(0);

	vector<int> T(1);
	int N; cin >> N >> T[0];

	for (int i = 1, x; i < N; ++i) {
		cin >> x;
		if (x < T.back()) T.emplace_back(x);
		else *lower_bound(T.begin(), T.end(), x, greater<int>()) = x;
	}
	cout << N - T.size();
	return 0;
}
```

``` java
import java.util.*;

public class Main {
	
    static int n;
    static ArrayList<Integer> v = new ArrayList<Integer>();
    static int[] dp = new int[2000];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();

        for (int i = 0; i < n; i++) {
            v.add(sc.nextInt());
        }

        // 순서를 뒤집어 '최장 증가 부분 수열' 문제로 변환
        Collections.reverse(v);

        // 다이나믹 프로그래밍을 위한 1차원 DP 테이블 초기화
        for (int i = 0; i < n; i++) {
            dp[i] = 1;
        }

        // 가장 긴 증가하는 부분 수열(LIS) 알고리즘 수행
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (v.get(j) < v.get(i)) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }

        // 열외해야 하는 병사의 최소 수를 출력
        int maxValue = 0;
        for (int i = 0; i < n; i++) {
            maxValue = Math.max(maxValue, dp[i]);
        }
        System.out.println(n - maxValue);
    }
}
```