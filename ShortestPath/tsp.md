
# Normal

1. Consider city 1 as the starting and ending point. Since the route is cyclic, we can consider any point as a starting point.
2. Generate all (n-1)! permutations of cities.
3. Calculate the cost of every permutation and keep track of the minimum cost permutation.
4. Return the permutation with minimum cost.

``` python
# Python3 program to implement traveling salesman 
# problem using naive approach. 
from sys import maxsize 
from itertools import permutations
V = 4
 
# implementation of traveling Salesman Problem 
def travellingSalesmanProblem(graph, s): 
 
    # store all vertex apart from source vertex 
    vertex = [] 
    for i in range(V): 
        if i != s: 
            vertex.append(i) 
 
    # store minimum weight Hamiltonian Cycle 
    min_path = maxsize 
    next_permutation=permutations(vertex)
    for i in next_permutation:
 
        # store current Path weight(cost) 
        current_pathweight = 0
 
        # compute current path weight 
        k = s 
        for j in i: 
            current_pathweight += graph[k][j] 
            k = j 
        current_pathweight += graph[k][s] 
 
        # update minimum 
        min_path = min(min_path, current_pathweight) 
         
    return min_path 
 
 
# Driver Code 
if __name__ == "__main__": 
 
    # matrix representation of graph 
    graph = [[0, 10, 15, 20], [10, 0, 35, 25], 
            [15, 35, 0, 30], [20, 25, 30, 0]] 
    s = 0
    print(travellingSalesmanProblem(graph, s))
```

``` cpp
// CPP program to implement traveling salesman
// problem using naive approach.
#include <bits/stdc++.h>
using namespace std;
#define V 4
 
// implementation of traveling Salesman Problem
int travllingSalesmanProblem(int graph[][V], int s)
{
    // store all vertex apart from source vertex
    vector<int> vertex;
    for (int i = 0; i < V; i++)
        if (i != s)
            vertex.push_back(i);
 
    // store minimum weight Hamiltonian Cycle.
    int min_path = INT_MAX;
    do {
 
        // store current Path weight(cost)
        int current_pathweight = 0;
 
        // compute current path weight
        int k = s;
        for (int i = 0; i < vertex.size(); i++) {
            current_pathweight += graph[k][vertex[i]];
            k = vertex[i];
        }
        current_pathweight += graph[k][s];
 
        // update minimum
        min_path = min(min_path, current_pathweight);
 
    } while (
        next_permutation(vertex.begin(), vertex.end()));
 
    return min_path;
}
 
// Driver Code
int main()
{
    // matrix representation of graph
    int graph[][V] = { { 0, 10, 15, 20 },
                       { 10, 0, 35, 25 },
                       { 15, 35, 0, 30 },
                       { 20, 25, 30, 0 } };
    int s = 0;
    cout << travllingSalesmanProblem(graph, s) << endl;
    return 0;
}
```

``` java
// Java program to implement 
// traveling salesman problem 
// using naive approach.
import java.util.*;
class GFG{
     
static int V = 4;
 
// implementation of traveling 
// Salesman Problem
static int travllingSalesmanProblem(int graph[][],
                                    int s)
{
  // store all vertex apart 
  // from source vertex
  ArrayList<Integer> vertex =
            new ArrayList<Integer>();
   
  for (int i = 0; i < V; i++)
    if (i != s)
      vertex.add(i);
 
  // store minimum weight 
  // Hamiltonian Cycle.
  int min_path = Integer.MAX_VALUE;
  do
  {
    // store current Path weight(cost)
    int current_pathweight = 0;
 
    // compute current path weight
    int k = s;
     
    for (int i = 0; 
             i < vertex.size(); i++) 
    {
      current_pathweight += 
              graph[k][vertex.get(i)];
      k = vertex.get(i);
    }
    current_pathweight += graph[k][s];
 
    // update minimum
    min_path = Math.min(min_path, 
                        current_pathweight);
 
  } while (findNextPermutation(vertex));
 
  return min_path;
}
 
// Function to swap the data 
// present in the left and right indices 
public static ArrayList<Integer> swap(
              ArrayList<Integer> data, 
              int left, int right) 
{ 
  // Swap the data 
  int temp = data.get(left); 
  data.set(left, data.get(right)); 
  data.set(right, temp); 
 
  // Return the updated array 
  return data; 
} 
   
// Function to reverse the sub-array 
// starting from left to the right 
// both inclusive 
public static ArrayList<Integer> reverse(
              ArrayList<Integer> data, 
              int left, int right) 
{ 
  // Reverse the sub-array 
  while (left < right) 
  { 
    int temp = data.get(left); 
    data.set(left++, 
             data.get(right)); 
    data.set(right--, temp); 
  } 
 
  // Return the updated array 
  return data; 
} 
   
// Function to find the next permutation 
// of the given integer array 
public static boolean findNextPermutation(
                      ArrayList<Integer> data) 
{  
  // If the given dataset is empty 
  // or contains only one element 
  // next_permutation is not possible 
  if (data.size() <= 1) 
    return false; 
 
  int last = data.size() - 2; 
 
  // find the longest non-increasing 
  // suffix and find the pivot 
  while (last >= 0) 
  { 
    if (data.get(last) < 
        data.get(last + 1)) 
    { 
      break; 
    } 
    last--; 
  } 
 
  // If there is no increasing pair 
  // there is no higher order permutation 
  if (last < 0) 
    return false; 
 
  int nextGreater = data.size() - 1; 
 
  // Find the rightmost successor 
  // to the pivot 
  for (int i = data.size() - 1; 
           i > last; i--) { 
    if (data.get(i) > 
        data.get(last)) 
    { 
      nextGreater = i; 
      break; 
    } 
  } 
 
  // Swap the successor and 
  // the pivot 
  data = swap(data, 
              nextGreater, last); 
 
  // Reverse the suffix 
  data = reverse(data, last + 1, 
                 data.size() - 1); 
 
  // Return true as the 
  // next_permutation is done 
  return true; 
} 
 
// Driver Code
public static void main(String args[])
{
  // matrix representation of graph
  int graph[][] = {{0, 10, 15, 20},
                   {10, 0, 35, 25},
                   {15, 35, 0, 30},
                   {20, 25, 30, 0}};
  int s = 0;
  System.out.println(
  travllingSalesmanProblem(graph, s));
}
}
 
// This code is contributed by adityapande88
```
# Backtracking

1. Consider city 1 (let say 0th node) as the starting and ending point. Since route is cyclic, we can consider any point as starting point.
2. Start traversing from the source to its adjacent nodes in dfs manner.
3. Calculate cost of every traversal and keep track of minimum cost and keep on updating the value of minimum cost stored value.
4. Return the permutation with minimum cost.

``` python
n = int(input())
graph = [list(map(int, input().split())) for _ in range(n)]
answer= []
visited = [False for _ in range(n)] 
  
# Function to find the minimum weight  
# Hamiltonian Cycle 
def tsp(now, count, cost): 
  
    # If last node is reached and it has  
    # a link to the starting node i.e  
    # the source then keep the minimum  
    # value out of the total cost of  
    # traversal and "ans" 
    # Finally return to check for  
    # more possible values 
    visited[now] = True
    if count == n-1 and graph[now][0]: 
        answer.append(cost + graph[now][0]) 
        return
  
    # BACKTRACKING STEP 
    # Loop to traverse the adjacency list 
    # of now node and increasing the count 
    # by 1 and cost by graph[now][i] value 
    for i in range(n): 
        if not visited[i] and graph[now][i]: 
            visited[i] = True # Mark as visited 
            tsp(i, count + 1, cost + graph[now][i])
            visited[i] = False # Mark ith node as unvisited 

# Driver code 
  
# Find the minimum weight Hamiltonian Cycle 
tsp(0, 0, 0) 

# ans is the minimum weight Hamiltonian Cycle 
print(min(answer))
```

``` cpp
// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 
#define V 4 
  
// Function to find the minimum weight Hamiltonian Cycle 
void tsp(int graph[][V], vector<bool>& v, int currPos, 
         int n, int count, int cost, int& ans) 
{ 
  
    // If last node is reached and it has a link 
    // to the starting node i.e the source then 
    // keep the minimum value out of the total cost 
    // of traversal and "ans" 
    // Finally return to check for more possible values 
    if (count == n && graph[currPos][0]) { 
        ans = min(ans, cost + graph[currPos][0]); 
        return; 
    } 
  
    // BACKTRACKING STEP 
    // Loop to traverse the adjacency list 
    // of currPos node and increasing the count 
    // by 1 and cost by graph[currPos][i] value 
    for (int i = 0; i < n; i++) { 
        if (!v[i] && graph[currPos][i]) { 
  
            // Mark as visited 
            v[i] = true; 
            tsp(graph, v, i, n, count + 1, 
                cost + graph[currPos][i], ans); 
  
            // Mark ith node as unvisited 
            v[i] = false; 
        } 
    } 
}; 
  
// Driver code 
int main() 
{ 
    // n is the number of nodes i.e. V 
    int n = 4; 
  
    int graph[][V] = { 
        { 0, 10, 15, 20 }, 
        { 10, 0, 35, 25 }, 
        { 15, 35, 0, 30 }, 
        { 20, 25, 30, 0 } 
    }; 
  
    // Boolean array to check if a node 
    // has been visited or not 
    vector<bool> v(n); 
    for (int i = 0; i < n; i++) 
        v[i] = false; 
  
    // Mark 0th node as visited 
    v[0] = true; 
    int ans = INT_MAX; 
  
    // Find the minimum weight Hamiltonian Cycle 
    tsp(graph, v, 0, n, 1, 0, ans); 
  
    // ans is the minimum weight Hamiltonian Cycle 
    cout << ans; 
  
    return 0; 
} 
```

``` java
// Java implementation of the approach 
class GFG  
{ 
  
    // Function to find the minimum weight  
    // Hamiltonian Cycle 
    static int tsp(int[][] graph, boolean[] v,  
                   int currPos, int n,  
                   int count, int cost, int ans)  
    { 
  
        // If last node is reached and it has a link 
        // to the starting node i.e the source then 
        // keep the minimum value out of the total cost 
        // of traversal and "ans" 
        // Finally return to check for more possible values 
        if (count == n && graph[currPos][0] > 0)  
        { 
            ans = Math.min(ans, cost + graph[currPos][0]); 
            return ans; 
        } 
  
        // BACKTRACKING STEP 
        // Loop to traverse the adjacency list 
        // of currPos node and increasing the count 
        // by 1 and cost by graph[currPos,i] value 
        for (int i = 0; i < n; i++)  
        { 
            if (v[i] == false && graph[currPos][i] > 0)  
            { 
  
                // Mark as visited 
                v[i] = true; 
                ans = tsp(graph, v, i, n, count + 1, 
                          cost + graph[currPos][i], ans); 
  
                // Mark ith node as unvisited 
                v[i] = false; 
            } 
        } 
        return ans; 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
  
        // n is the number of nodes i.e. V 
        int n = 4; 
  
        int[][] graph = {{0, 10, 15, 20}, 
                         {10, 0, 35, 25}, 
                         {15, 35, 0, 30}, 
                         {20, 25, 30, 0}}; 
  
        // Boolean array to check if a node 
        // has been visited or not 
        boolean[] v = new boolean[n]; 
  
        // Mark 0th node as visited 
        v[0] = true; 
        int ans = Integer.MAX_VALUE; 
  
        // Find the minimum weight Hamiltonian Cycle 
        ans = tsp(graph, v, 0, n, 1, 0, ans); 
  
        // ans is the minimum weight Hamiltonian Cycle 
        System.out.println(ans); 
    } 
} 
  
// This code is contributed by Rajput-Ji 
```
