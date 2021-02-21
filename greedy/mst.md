## Minimum Spanning Tree (MST)

### Kruskal's Algo

``` python

def find(parent, x):
    if x != parent[x]:
        parent[x] = find(parent, parent[x])
    return parent[x]

def union(parent, a, b):
    x, y = find(parent, a), find(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

v, e = map(int, input().split())
parent = [i for i in range(v+1)]

# All edges and final cost
graph = []
result = 0

for _ in range(e):
    a, b, c = map(int, input().split())
    graph.append((c, a, b)) # NOTICE the order

# Sort w/ cost
graph.sort()

for edges in graph:
    c, a, b = edges
    if find(parent, a) != find(parent, b):
        union(parent, a, b)
        result += c

print(result)
```

### Prim's Algo.

``` python

```