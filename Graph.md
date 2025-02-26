# Graphs – Complete Guide for Interviews

## Key Terminology
- **Vertex**: A node in the graph.
- **Edge**: A connection between two vertices.
- **Directed Graph**: The edges have a direction.
- **Undirected Graph**: The edges do not have a direction.
- **Weight**: The cost associated with traveling along an edge.
- **Adjacency Matrix**: A 2D array where matrix[i][j] = 1 if there’s an edge between vertex i and vertex j.
- **Adjacency List**: A list where each index represents a vertex, and each element is a list of adjacent vertices.
- **Connected Graph**: A graph in which there’s a path between every pair of vertices.
- **Cycle**: A path that starts and ends at the same vertex without visiting any vertex twice.

## Graph Representation

### A. Adjacency List Representation
```csharp
class Graph {
    Dictionary<int, List<int>> adjacencyList = new Dictionary<int, List<int>>();

    public void AddEdge(int u, int v) {
        if (!adjacencyList.ContainsKey(u)) adjacencyList[u] = new List<int>();
        adjacencyList[u].Add(v);
    }
}
```

### B. Adjacency Matrix Representation
```csharp
int[,] adjacencyMatrix = new int[5, 5];  // For a 5-node graph
adjacencyMatrix[0, 1] = 1;  // Edge from node 0 to node 1
```

## Graph Traversal Techniques

### A. Depth-First Search (DFS)
**Recursive DFS:**
```csharp
void DFS(Dictionary<int, List<int>> graph, int node, HashSet<int> visited) {
    if (visited.Contains(node)) return;
    visited.Add(node);
    Console.WriteLine(node);  // Process node
    foreach (int neighbor in graph[node]) {
        DFS(graph, neighbor, visited);
    }
}
```

**Iterative DFS (using a stack):**
```csharp
void IterativeDFS(Dictionary<int, List<int>> graph, int start) {
    Stack<int> stack = new Stack<int>();
    HashSet<int> visited = new HashSet<int>();
    stack.Push(start);
    while (stack.Count > 0) {
        int node = stack.Pop();
        if (!visited.Contains(node)) {
            Console.WriteLine(node);  // Process node
            visited.Add(node);
            foreach (int neighbor in graph[node]) {
                stack.Push(neighbor);
            }
        }
    }
}
```

### B. Breadth-First Search (BFS)
**Using a queue:**
```csharp
void BFS(Dictionary<int, List<int>> graph, int start) {
    Queue<int> queue = new Queue<int>();
    HashSet<int> visited = new HashSet<int>();
    queue.Enqueue(start);
    visited.Add(start);
    while (queue.Count > 0) {
        int node = queue.Dequeue();
        Console.WriteLine(node);  // Process node
        foreach (int neighbor in graph[node]) {
            if (!visited.Contains(neighbor)) {
                queue.Enqueue(neighbor);
                visited.Add(neighbor);
            }
        }
    }
}
```

## Detecting Cycles in a Graph

### A. Undirected Graph (Using DFS)
```csharp
bool HasCycleUndirected(Dictionary<int, List<int>> graph, int node, int parent, HashSet<int> visited) {
    visited.Add(node);
    foreach (int neighbor in graph[node]) {
        if (!visited.Contains(neighbor)) {
            if (HasCycleUndirected(graph, neighbor, node, visited)) return true;
        } else if (neighbor != parent) {
            return true;  // Cycle detected
        }
    }
    return false;
}
```
This function `HasCycleUndirected` is used to detect cycles in an undirected graph using Depth-First Search (DFS). The graph is represented as a dictionary where each key is a node, and the value is a list of its neighbors. The function takes four parameters: the graph, the current node, the parent node, and a set of visited nodes.

1. **Mark the Current Node as Visited**: The function starts by adding the current node to the `visited` set to keep track of nodes that have already been explored.

2. **Iterate Through Neighbors**: It then iterates through each neighbor of the current node. For each neighbor, it checks if the neighbor has already been visited.

3. **Recursive DFS Call**: If the neighbor has not been visited, the function makes a recursive call to `HasCycleUndirected` with the neighbor as the new current node and the current node as the parent. If this recursive call returns `true`, it means a cycle has been detected, and the function returns `true`.

4. **Cycle Detection**: If the neighbor has been visited and is not the parent of the current node, it indicates a cycle, and the function returns `true`.

5. **No Cycle Found**: If none of the neighbors lead to a cycle, the function returns `false`.

This approach ensures that each node is visited only once, making the algorithm efficient. The use of a parent node helps to distinguish between a back edge (which indicates a cycle) and a tree edge (which does not).

### B. Directed Graph (Using DFS and visited states)
```csharp
bool HasCycleDirected(Dictionary<int, List<int>> graph, int node, HashSet<int> visited, HashSet<int> recStack) {
    if (!visited.Contains(node)) {
        visited.Add(node);
        recStack.Add(node);
        foreach (int neighbor in graph[node]) {
            if (!visited.Contains(neighbor) && HasCycleDirected(graph, neighbor, visited, recStack)) {
                return true;
            } else if (recStack.Contains(neighbor)) {
                return true;  // Cycle detected
            }
        }
    }
    recStack.Remove(node);
    return false;
}
```
The function `HasCycleDirected` is designed to detect cycles in a directed graph using Depth-First Search (DFS). The graph is represented as a dictionary where each key is a node, and the value is a list of its neighbors. The function takes four parameters: the graph, the current node, a set of visited nodes, and a recursion stack (`recStack`).

1. **Check if Node is Visited**: The function first checks if the current node has already been visited. If it has not, the node is added to both the `visited` set and the `recStack`.

2. **Iterate Through Neighbors**: It then iterates through each neighbor of the current node. For each neighbor, it checks two conditions:
   - If the neighbor has not been visited, the function makes a recursive call to `HasCycleDirected` with the neighbor as the new current node. If this recursive call returns `true`, it means a cycle has been detected, and the function returns `true`.
   - If the neighbor is already in the `recStack`, it indicates a cycle, and the function returns `true`.

3. **Remove Node from Recursion Stack**: After exploring all neighbors, the node is removed from the `recStack` to backtrack.

4. **No Cycle Found**: If none of the neighbors lead to a cycle, the function returns `false`.

This approach ensures that each node is visited only once, and the use of the recursion stack helps to detect back edges, which indicate cycles in directed graphs. The algorithm is efficient and effectively identifies cycles by leveraging the properties of DFS and the recursion stack.

## Shortest Path Algorithms

### A. Dijkstra’s Algorithm (For Weighted Graphs)
```csharp
void Dijkstra(int[,] graph, int src, int n) {
    int[] dist = new int[n];  // Distance array
    bool[] visited = new bool[n];  // Visited set
    for (int i = 0; i < n; i++) dist[i] = int.MaxValue;
    dist[src] = 0;
    for (int i = 0; i < n - 1; i++) {
        int u = MinDistance(dist, visited);  // Find the minimum distance vertex
        visited[u] = true;
        for (int v = 0; v < n; v++) {
            if (!visited[v] && graph[u, v] != 0 && dist[u] != int.MaxValue && dist[u] + graph[u, v] < dist[v]) {
                dist[v] = dist[u] + graph[u, v];
            }
        }
    }
}

int MinDistance(int[] dist, bool[] visited) {
    int min = int.MaxValue, minIndex = -1;
    for (int v = 0; v < dist.Length; v++) {
        if (!visited[v] && dist[v] <= min) {
            min = dist[v];
            minIndex = v;
        }
    }
    return minIndex;
}
```
The function `Dijkstra` implements Dijkstra's algorithm to find the shortest paths from a source vertex to all other vertices in a given graph. The graph is represented as a 2D array (`int[,] graph`), where `graph[u, v]` holds the weight of the edge from vertex `u` to vertex `v`. The function takes three parameters: the graph, the source vertex (`src`), and the number of vertices (`n`).

1. **Initialization**: 
   - An array `dist` is created to store the shortest distance from the source to each vertex. Initially, all distances are set to `int.MaxValue` (representing infinity), except for the source vertex, which is set to 0.
   - A boolean array `visited` is used to keep track of vertices that have been processed.

2. **Main Loop**:
   - The algorithm runs `n-1` times, where `n` is the number of vertices. In each iteration, it finds the vertex `u` with the minimum distance from the source that has not been visited yet. This is done using the helper function `MinDistance`.

3. **Update Distances**:
   - Once the vertex `u` is selected, it is marked as visited.
   - The algorithm then iterates through all vertices `v`. For each vertex `v`, it checks if there is an edge from `u` to `v` (`graph[u, v] != 0`), if `v` has not been visited, and if the distance to `u` is not infinity. If these conditions are met and the distance to `v` through `u` is shorter than the current known distance, the distance is updated.

4. **Helper Function `MinDistance`**:
   - This function finds the vertex with the minimum distance from the source that has not been visited. It iterates through the `dist` array and returns the index of the vertex with the smallest distance.

By the end of the algorithm, the `dist` array contains the shortest distances from the source vertex to all other vertices in the graph. Dijkstra's algorithm is efficient for graphs with non-negative weights and is widely used in network routing and geographical mapping applications.
### C. Dijkstra’s Algorithm (Using Priority Queue)
```csharp
void DijkstraWithPriorityQueue(int[,] graph, int src, int n) {
    int[] dist = new int[n];
    for (int i = 0; i < n; i++) dist[i] = int.MaxValue;
    dist[src] = 0;

    var pq = new PriorityQueue<int, int>();
    pq.Enqueue(src, 0);

    while (pq.Count > 0) {
        pq.TryDequeue(out int u , out int currDist)

        if (currdist > dist[u]) continue;

        for (int v = 0;v<n;v++) {
            
            if (graph[u,v]!=0 && dist[u] + graph[u,v] < dist[v]) {
                dist[v] = dist[u] + graph[u,v];
                pq.Enqueue(v, dist[v]);
            }
        }
    }

    // Output the shortest distances
    for (int i = 0; i < n; i++) {
        Console.WriteLine($"Distance from {src} to {i} is {dist[i]}");
    }
}
```

---

### **1. Comparison with Previous Approach
- **Efficiency**: The priority queue approach is more efficient than the previous approach using a simple array for finding the minimum distance vertex. The priority queue allows for faster extraction of the minimum element and updating of distances, leading to an overall time complexity of \(O((V + E) \log V)\), where \(V\) is the number of vertices and \(E\) is the number of edges.
- **Implementation**: The priority queue approach uses a `PriorityQueue` to maintain the vertices to be processed, sorted by their current known shortest distance. This reduces the need for a separate `MinDistance` function and simplifies the main loop.
- **Scalability**: The priority queue approach scales better for larger graphs with many edges, as it handles the frequent updates and extractions more efficiently than the simple array-based approach.



### **2. Why No `visited` Array is Needed**
- **Duplicate Entries in the Priority Queue**:
  - A vertex can be added to the priority queue multiple times if its distance is updated (e.g., if a shorter path is found).
  - However, when a vertex is dequeued, only the entry with the smallest distance is processed. All other entries for the same vertex are ignored because their distances are larger than the current known shortest distance.

- **Implicit Handling of Visited Vertices**:
  - When a vertex is dequeued, its distance is finalized (i.e., it will not change again). This is because Dijkstra's algorithm guarantees that the shortest distance to a vertex is found the first time it is dequeued (assuming non-negative edge weights).
  - Any subsequent entries for the same vertex in the priority queue will have larger distances and will be skipped.

---

### **3. Example**
Consider the following graph:

```
    1
A ---- B
|     / |
4|   /1 |2
| /    |
C ---- D
    3
```

- Suppose the source vertex is `A`.
- The priority queue will initially contain `(A, 0)`.
- When `A` is dequeued, its neighbors `B` and `C` are added to the queue with distances `1` and `4`, respectively.
- Next, `B` is dequeued (distance `1`), and its neighbor `D` is added to the queue with distance `3` (`1 + 2`).
- Then, `D` is dequeued (distance `3`), and its neighbor `C` is added to the queue with distance `6` (`3 + 3`).
- Finally, `C` is dequeued (distance `4`). The entry `(C, 6)` in the queue is ignored because `4` is smaller than `6`.

At no point do we need a `visited` array because the priority queue ensures that each vertex is processed only once with its shortest distance.

---

### **4. Comparison with the Linear Search Implementation**
In the **linear search implementation** of Dijkstra's algorithm (without a priority queue), a `visited` array is necessary because:
- The algorithm explicitly iterates over all vertices to find the one with the smallest distance.
- Without a `visited` array, the algorithm might reprocess vertices that have already been finalized, leading to incorrect results.

---

### **5. When a `visited` Array Might Still Be Useful**
In some cases, a `visited` array can still be used to:
- Optimize memory usage by avoiding duplicate entries in the priority queue.
- Track which vertices have been processed for debugging or additional logic.

However, it is **not strictly necessary** for the correctness of the algorithm when using a priority queue.

---

### B. Floyd-Warshall Algorithm
```csharp
void FloydWarshall(int[,] dist, int n) {
    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (dist[i, k] + dist[k, j] < dist[i, j]) {
                    dist[i, j] = dist[i, k] + dist[k, j];
                }
            }
        }
    }
}
```
The function `FloydWarshall` implements the Floyd-Warshall algorithm, which is used to find the shortest paths between all pairs of vertices in a given weighted graph. The graph is represented as a 2D array (`int[,] dist`), where `dist[i, j]` holds the weight of the edge from vertex `i` to vertex `j`. The function takes two parameters: the distance matrix (`dist`) and the number of vertices (`n`).

1. **Initialization**:
   - The `dist` matrix is assumed to be initialized such that `dist[i, j]` is the direct distance between vertices `i` and `j`. If there is no direct edge between `i` and `j`, `dist[i, j]` should be set to a large value (representing infinity), except for the diagonal elements `dist[i, i]`, which should be zero.

2. **Triple Nested Loop**:
   - The algorithm uses three nested loops to iterate over all pairs of vertices `(i, j)` for each intermediate vertex `k`.
   - The outer loop iterates over each vertex `k`, considering it as an intermediate vertex.
   - The middle and inner loops iterate over all pairs of vertices `(i, j)`.

3. **Update Distances**:
   - For each pair of vertices `(i, j)`, the algorithm checks if the path from `i` to `j` through the intermediate vertex `k` is shorter than the current known path from `i` to `j`.
   - If `dist[i, k] + dist[k, j] < dist[i, j]`, it updates `dist[i, j]` to the new shorter distance `dist[i, k] + dist[k, j]`.

By the end of the algorithm, the `dist` matrix contains the shortest distances between all pairs of vertices. The Floyd-Warshall algorithm is efficient for dense graphs and can handle negative weights, provided there are no negative weight cycles. It is widely used in applications such as network routing, urban traffic planning, and solving the all-pairs shortest path problem in various domains.

## Topological Sorting (For Directed Acyclic Graphs - DAGs)

### Kahn’s Algorithm (BFS-based)
```csharp
List<int> TopologicalSort(Dictionary<int, List<int>> graph, int n) {
    int[] inDegree = new int[n];
    foreach (var node in graph.Keys) {
        foreach (var neighbor in graph[node]) {
            inDegree[neighbor]++;
        }
    }

    Queue<int> queue = new Queue<int>();
    for (int i = 0; i < n; i++) {
        if (inDegree[i] == 0) queue.Enqueue(i);
    }

    List<int> topoOrder = new List<int>();
    while (queue.Count > 0) {
        int node = queue.Dequeue();
        topoOrder.Add(node);
        foreach (int neighbor in graph[node]) {
            if (--inDegree[neighbor] == 0) queue.Enqueue(neighbor);
        }
    }

    return topoOrder;
}
```
The function `TopologicalSort` performs a topological sort on a directed acyclic graph (DAG). The graph is represented as a dictionary where each key is a node, and the value is a list of its neighbors. The function takes two parameters: the graph and the number of nodes (`n`).

1. **Calculate In-Degrees**:
   - An array `inDegree` is created to store the in-degree (number of incoming edges) of each node. Initially, all in-degrees are set to 0.
   - The function iterates over each node in the graph and its neighbors, incrementing the in-degree of each neighbor.

2. **Initialize Queue**:
   - A queue is used to keep track of nodes with an in-degree of 0 (nodes with no incoming edges).
   - The function iterates over all nodes, and if a node's in-degree is 0, it is enqueued.

3. **Process Nodes**:
   - A list `topoOrder` is created to store the topological order of the nodes.
   - While the queue is not empty, the function dequeues a node, adds it to `topoOrder`, and iterates over its neighbors.
   - For each neighbor, the in-degree is decremented. If the in-degree of a neighbor becomes 0, it is enqueued.

4. **Return Topological Order**:
   - After processing all nodes, the function returns the `topoOrder` list, which contains the nodes in topologically sorted order.

Topological sorting is used in scenarios where you need to order tasks based on dependencies, such as task scheduling, course prerequisites, and resolving symbol dependencies in linkers. The algorithm ensures that for every directed edge `u -> v`, node `u` appears before node `v` in the topological order.

## Common Interview Questions on Graphs
- Find all connected components in an undirected graph.
- Clone a graph (Deep Copy of an Undirected Graph).
- Word Ladder (Shortest path transformation from one word to another).
- Find bridges in a graph (Edges whose removal increases the number of connected components).
- Check if a graph is bipartite (2-colorable).
- Network Delay Time (Find the time taken for all nodes to receive a signal from a starting node).
- Strongly Connected Components (Kosaraju’s or Tarjan’s Algorithm).

## Summary Notes for Graphs
- **Graph Representations**: Adjacency List, Adjacency Matrix.
- **Traversal**: DFS (Recursive/Iterative), BFS (Queue-based).
- **Cycle Detection**: DFS-based for directed and undirected graphs.
- **Shortest Path**: Dijkstra (Single Source), Floyd-Warshall (All-Pairs).
- **Topological Sorting**: Kahn’s Algorithm (BFS-based).

## Tricks to Identify Graph Problems
1. **Relationships Between Entities**: If the problem talks about relationships or connections between objects/nodes.
2. **Paths or Shortest Path**: If the problem mentions finding the shortest path, minimum steps, or transformation from one state to another.
3. **Reachability or Connectivity**: If the problem asks whether it's possible to reach one node from another or if the entire graph is connected.
4. **Islands, Groups, or Clusters**: Problems that mention disconnected groups or islands.
5. **Cycle Detection**: If the problem asks whether there is a cycle or loop in the structure.
6. **Topological Order or Dependencies**: If the problem mentions ordering tasks or resolving dependencies.
7. **Transformation or State Change**: Problems that describe converting one state to another with allowed moves.
8. **Grid or Matrix**: Problems with a grid of cells that you need to explore or navigate.
9. **Network Flow or Maximum Flow**: Problems involving flow capacities and finding the maximum flow in a system.
10. **Bipartite or Coloring Problems**: If the problem involves dividing nodes into two or more groups or checking for conflicts.
11. **Traveling Salesman Problem (TSP)**: If the problem involves visiting all nodes exactly once and returning to the start.
12. **Strongly Connected Components (SCC)**: If the problem involves finding strongly connected components in a directed graph.
13. **Weighted Graphs and Minimum Spanning Tree (MST)**: If the problem asks for the minimum cost to connect all nodes.

### Tips to Recognize Graph Problems Quickly
- Look for connections/relationships: If entities are connected, it’s probably a graph problem.
- Paths or reachability: Any mention of paths, transformations, or shortest distances is a strong graph clue.
- Grid navigation: Grids are often modeled as graphs where each cell is a node and adjacent cells are edges.
- Dependencies or ordering: Dependencies almost always lead to topological sorting or cycle detection in graphs.
- Flow and capacities: Think of network flow algorithms for problems involving flows and capacities.
