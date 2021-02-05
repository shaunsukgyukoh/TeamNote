## Bellman-Ford algo

``` python
# Bellman-Ford implementation from MIT 6006 course lesson #17
import math
import networkx as nx

# utility: Graph
class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.edges = []
    
    def add_edge(self, edge):
        self.edges.append(edge)
        
    def __str__(self):
        result = ''
        for edge in self.edges:
            result += f'{v}: {str(edge)}, \n'
        return result

def bellmanFord(graph, s):
    """
    Idea behind bellman-ford vs dijkstra:
    
    They both can be used to find shortest path. But their approach is different.

    Dijkstra is a greedy algorithm, which means it makes 'best optimal answer' for each given step.
    But it fails when it encounters negative weights. Why? Because you can improve the weight by adding
    one more iteration of relaxing all the edges.

    However, Bellman-Ford is not a greedy algorithm. It just inspects for all the possible improvements
    simply by looping over edges |V| - 1 times to get the best weight for 'shortest simple path'(SSP).
    Then why |V| - 1 times? The length of the longest simple path(path w/o cycle) would be |V| - 1.
    For example, you need 2 edges to connect 3 vertices, otherwise, there exists a negative cycle.
    """
    d = dict.fromkeys(graph.V, math.inf) # distance pair 
                                         # will have default value of Infinity
    pi = dict.fromkeys(graph.V, None) # map of parent vertex
    
    # initialize
    d[s] = 0
    
    def relax(u, v, w):
        if d[v] > d[u] + w:
            d[v] = d[u] + w
            pi[v] = u
    
    # The length of the longest simple path(path w/o cycle) would be |V| - 1.
    # For example, you need 2 edges to connect 3 vertices.
    # Otherwise, there exists a negative cycle.
    for i in graph.V[:-1]:
        for u, v, w in graph.edges:
            relax(u, v, w)
            
    for u, v, w in graph.edges:
        # even after relaxing all the edges for |V| - 1 times,
        # we still have the posibillity to improve the existing path
        # this means there are negative cycles
        if d[v] > d[u] + w:
            return f'there exists a negetive cycle!'
                
    return d, pi

def shortest_path(s, t):
    try:
        d, pi = bellmanFord(g, s)
    except ValueError:
        return 'you can\'t find shortest path if the graph has negative cycle!'
    
    path = [t]
    current = t
    
    # if parent pointer is None,
    # then it's the source vertex
    while pi[current]:
        path.insert(0, pi[current])
        # set current to parent
        current = pi[current]
    
    if s not in path:
        return f'unable to find shortest path staring from "{s}" to "{t}"'
    
    return f'{" > ".join(path)}'

g = Graph(['A', 'B', 'C', 'D', 'E'])

# graph with negative cycle
nc_edges = [('A', 'B', 5), ('B', 'C', -1), ('C', 'D', 2), ('D', 'B', -2), ('C', 'E', 4)]

# w/o negative cycles
edges = [\
    ('A', 'B', 10), ('A', 'C', 3), ('B', 'C', 1), ('C', 'B', 4), \
    ('B', 'D', 2), ('C', 'D', 8), ('D', 'E', 7), ('E', 'D', 9), ('C', 'E', 2)]

# used for both finding shortest path and drawing graph
current_edge_group = edges

for edge in current_edge_group:
    g.add_edge(edge)

print( shortest_path('A', 'E') )

G = nx.DiGraph()
G.add_weighted_edges_from(current_edge_group)
nx.draw(G, with_labels = True, node_color='b', font_color='w')
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