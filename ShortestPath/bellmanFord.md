## Bellman-Ford algo

``` python
## 방법 1: graph elem: graph[a] = [(b, c)]
import sys
def bellmanFord(start):
    distance[start] = 0
    for k in range(N):
        for a in range(1, N+1):
            for b, c in graph[a]:
                if distance[b] > distance[a] + c:
                    distance[b] = distance[a] + c
                    if k == N-1:
                        return True
    return False

def bellmanFord2(start):
    distance[start] = 0
    for k in range(N):
        for a in range(1, N+1):
            for b, c in graph[a]:
                if distance[b] > distance[a] + c:
                    distance[b] = distance[a] + c

    for a in range(1, N+1):
        for b, c in graph[a]:
            if distance[b] > distance[a] + c:
                return True
    return False

for _ in range(int(sys.stdin.readline())):
    N, M, W = map(int, sys.stdin.readline().split())
    graph = [[] for _ in range(N+1)]
    distance = [1e9] * (N+1)
    # both way`
    for _ in range(M):
        s, e, t = map(int, sys.stdin.readline().split())
        graph[s].append((e, t))
        graph[e].append((s, t))
    # one way
    for _ in range(W):
        s, e, t = map(int, sys.stdin.readline().split())
        graph[s].append((e, -t))
    print('YES' if bellmanFord(1) else 'NO')
    print(distance)
    distance = [1e9] * (N+1)
    print('YES' if bellmanFord2(1) else 'NO')
    print(distance)

'''
2
3 3 1
1 2 2
1 3 4
2 3 1
3 1 3
3 2 1
1 2 3
2 3 4
3 1 8

NO
[1000000000.0, 0, 2, 3]
NO
[1000000000.0, 0, 2, 3]
YES
[1000000000.0, -2, 1, 6]
YES
[1000000000.0, -3, 1, 5]
'''

## 방법 2: graph elem: (a, b, c)
import sys

input = sys.stdin.readline
for _ in range(int(input())):
    N, M, W = map(int, input().split())
    graph = []
    dist = [0, 0] + [9**9] * (N-1)
    for _ in range(M):
        n1, n2, w = map(int, input().split())
        graph.append([n1, n2, w])
        graph.append([n2, n1, w])
    for _ in range(W):
        n1, n2, w = map(int, input().split())
        graph.append([n1, n2, -w])

    for _ in range(N):
        for s, e, w in graph:
            dist[e] = min(dist[e], dist[s]+w)
    for s, e, w in graph:
        if dist[e] > dist[s]+w:
            print('YES')
            break
    else:
        print('NO')
```

``` cpp
#include <bits/stdc++.h>
#define INF 0x3f3f3f3f
using namespace std;

class Graph{
private:
        int V;
        //lista de aristas, con formato <peso,origen,destino>
        vector<pair<int,pair<int,int> > > edges;
        bool hasNegativeCycle = false;
public:
    Graph(int V);
    void addEdge(int u,int v,int w);
    void bellmanFord(int src);
    //void printDistances();
};
Graph::Graph(int V){
    this->V = V;
}
void Graph::addEdge(int u,int v,int w){
     //edges.push_back(make_pair(w,make_pair(u,v)));
    edges.push_back({w,{u,v}});
}
void Graph::bellmanFord(int src){
    //arreglo de distancias seteado inicialmente como infinito
    vector<int> dist(this->V,INF);
    //la distancia a si mismo debe ser 0
    dist[src] = 0;
    vector<pair<int,pair<int,int> > >::iterator it;

    for(int i=1;i<this->V;i++){
        for(it = edges.begin();it!=edges.end();++it){
            int u = it->second.first;
            int v = it->second.second;
            int w = it->first;
             //Relajacion de las aristas
            if(dist[u] + w < dist[v]){
                dist[v] = dist[u] + w;
            }
        }
    }
        //¿Quedó alguna arista sin relajardespués de las V*E relajaciones?  
        // Quiere decir que el grafo tiene ciclos internos de peso negativo, el algoritmo Bellman Ford no funcionará correctamente. 
    for(it = edges.begin();it!=edges.end();++it){
        int u = it->second.first;
        int v = it->second.second;
        int w = it->first;
        if(dist[u] + w < dist[v]){
            this->hasNegativeCycle = true;
            //return false
        }
    }
        //Imprime todas las distancias desde el origen hasta todos los vertices. 
    if(!hasNegativeCycle){
        for(int i=0;i<V;i++){
            cout << i << " - " << dist[i] << endl;
        }
    }
}
int main(){
    int V = 5;
    //int E; cuantas aristas
    Graph g(V);
    g.addEdge(0,1,7);
    g.addEdge(0,4,6);
    g.addEdge(1,2,9);
    g.addEdge(1,3,-3);
    g.addEdge(2,0,2);
    g.addEdge(2,3,7);
    g.addEdge(3,4,-2);
    g.addEdge(4,1,8);
    g.addEdge(4,2,-4);
    g.addEdge(4,3,5);

    g.bellmanFord(2);
    return 0;
}
```

``` cpp
#include<stdio.h>
#include<algorithm>
#include<queue>
#include<vector>
using namespace std;
 
int dist[101];
 
struct Edge {
    int s;
    int e;
    int val;
    Edge(int a, int b, int c) {
        s = a;
        e = b;
        val = c;
    }
};
 
int main() {
    freopen("input.txt", "rt", stdin);
    vector<Edge> Ed;
    int i, n, m, a, b, c, j;
 
    scanf("%d %d", &n, &m);
    for (i = 1; i <= m; i++) {
        scanf("%d %d %d", &a, &b, &c);
        Ed.push_back(Edge(a, b, c));
    }
 
    for (i = 1; i <= n; i++) {
        dist[i] = 2147000000;
    }
 
    dist[1] = 0;
    for (i = 1; i < n; i++) {
        for (j = 0; j < Ed.size(); j++) {
            int s = Ed[j].s;
            int e = Ed[j].e;
            int w = Ed[j].val;
            if (dist[s] != 2147000000 && dist[s] + w < dist[e]) {
                dist[e] = dist[s] + w;
            }
        }
    }
 
    for (j = 0; j < Ed.size(); j++) {
        int u = Ed[j].s;
        int v = Ed[j].e;
        int w = Ed[j].val;
        if (dist[u] != 2147000000 && dist[u] + w < dist[v]) {
            printf("-1\n");
            exit(0);
        }
    }
    printf("%d\n", dist[n]);
 
    return 0;
}

```

``` java
import java.util.Arrays;

public class BellmanFord {

    public static final int INF = Integer.MAX_VALUE;

    public static void main(String[] args) {
        int num = 5;
        int[][] adj = new int[][] {
                {0, -4, 5, 2, 3},
                {INF, 0, INF, -1, INF},
                {INF, INF, 0, -7, INF},
                {INF, INF, INF, 0, 6},
                {INF, INF, INF, -4, 0},
        };
        int src = 0;
        int dst = 1;

        solve(num, adj, src, dst);
    }

    public static void solve(int num, int[][] adj, int src, int dst) {
        int[] dists = new int[num];
        Arrays.fill(dists, INF);
        dists[src] = 0;

        for(int v=0; v < num; ++v) {
            for(int w=0; w < num; ++w) {
                if(adj[v][w] != INF)
                    dists[w] = Math.min(dists[w], dists[v] + adj[v][w]);
            }
        }

        for(int i=0; i< num; ++i)
            System.out.println(dists[i]);
    }
}
```