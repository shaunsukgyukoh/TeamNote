## Queue and Stack

### Queue

``` python
from collections import deque

q = deque()

q.append(2)
q.append(5)
q.append(1)
q.popleft()
q.append(3)

print(q)
```

``` cpp
#include <bits/stdc++.h>

using namespace std;

queue<int> q;

int main(void){
    q.push(2);
    q.push(5);
    q.push(1);
    q.pop();
    q.push(3);

    while(!q.empty()){
        cout << q.front() << ' ';
        q.pop();
    }
}
```

``` java
import java.util.*;

public class Main {
    public static void main(String[] args){
        Queue<Integer> q = new LinkedList<>();

        q.offer(2);
        q.offer(5);
        q.offer(1);
        q.poll();
        q.offer(3);

        while(!q.empty()){
            System.out.print(q.poll() + " ");
        }
    }
}
```

### Stack

``` python
from collections import deque

s = deque()

s.append(2)
s.append(5)
s.append(1)
s.pop()
s.append(3)

print(s[::-1]) # from top
print(s) # from bottom
```

``` cpp
#include <bits/stdc++.h>

using namespace std;

stack<int> s;

int main(void){
    s.push(2);
    s.push(5);
    s.push(1);
    s.pop();
    s.push(3);
    
    while (!s.empty()){
        cout << s.top() << ' ';
        s.pop();
    }
}
```

``` java
import java.util.*;

public class Main {
    public static void main(String[] args){
        Stack<Integer> s = new Stack<>();
        s.push(2);
        s.push(5);
        s.push(1);
        s.pop();
        s.push(3);

        while (!s.empty()){
            System.out.print(s.peek() + " ");
            s.pop();
        }
    }
}
```