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
