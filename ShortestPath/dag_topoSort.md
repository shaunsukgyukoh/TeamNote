## DAG / Topological Sort

- Scheduling
- Can have multiple outputs

- Indegree: Certain node's incoming # of edges
1. Insert node w/ 0 indegree into queue
2. while q: 
    1. Delete outgoing edges from that node
    2. Insert new node w/ 0 indegree (if q empties before looping V times, there's cycle)

``` python
from collections import deque

v, e = map(int, input().split())
# init indegree
indegree = [0] * (v+1)
graph = [[] for _ in range(v+1)]

for _ in range(e):
    a, b = map(int, input().split())
    graph[a].append(b)
    indegree[b] += 1

def topo():
    result = []
    q = deque()

    # In the beginning, add all 0 indegree node into queue
    for i in range(1, v+1):
        if indegree[i] == 0:
            q.append(i)

    while q:
        now = q.popleft()
        result.append(now)
        for i in graph[now]:
            indegree[i] -= 1
            if indegree[i] == 0:
                q.append(i)

    print(' '.join(str(i) for i in result))
```
