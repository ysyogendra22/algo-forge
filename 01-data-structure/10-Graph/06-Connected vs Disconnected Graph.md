# Connected vs Disconnected Graph

#### 1. Definition — Must Know

1. **Connected Graph** → Every vertex can reach every other vertex.
2. **Disconnected Graph** → At least one vertex cannot reach some other vertex.

This terminology mainly applies directly to **undirected graphs**.

#### 2. Connected Graph — Must Know

```text
A ----- B
|       |
C ----- D
```

Every node is reachable from every other node.

```text
A → B
A → C
A → D
```

So the graph has:

```text
1 Connected Component
```

#### 3. Disconnected Graph — Must Know

```text
A ----- B       D ----- E
      |
      C

          F
```

There are separate groups:

```text
Component 1 → A, B, C
Component 2 → D, E
Component 3 → F
```

So:

```text
Connected Components = 3
```

An isolated vertex like `F` is also its own component.

#### 4. Connected Component — Must Know

1. A **Connected Component** is a group of vertices that can reach each other.
2. A connected graph has exactly **1 component**.
3. A disconnected graph has **2 or more components**.

#### 5. Finding Connected Components — Must Know

Use **DFS or BFS**.

Logic:

```text
components = 0

for every vertex:
    if vertex is not visited:
        run DFS/BFS
        components++
```

Each new DFS/BFS discovers one complete component.

#### 6. Kotlin Implementation — Must Know

```kotlin
fun countComponents(
    n: Int,
    graph: Map<Int, List<Int>>
): Int {

    val visited = BooleanArray(n)
    var components = 0

    fun dfs(node: Int) {
        visited[node] = true

        for (neighbor in graph[node].orEmpty()) {
            if (!visited[neighbor]) {
                dfs(neighbor)
            }
        }
    }

    for (node in 0 until n) {
        if (!visited[node]) {
            dfs(node)
            components++
        }
    }

    return components
}
```

#### 7. Complexity — Must Know

```text
Time  → O(V + E)
Space → O(V)
```

1. Every vertex is visited once.
2. Every edge is processed during traversal.
3. `visited` and DFS/BFS storage can require `O(V)`.

#### 8. Directed Graphs — Good to Know

Connectivity is more specific for directed graphs:

1. **Strongly Connected** → Every vertex can reach every other vertex following edge directions.
2. **Weakly Connected** → Connected if edge directions are ignored.
3. **Strongly Connected Component (SCC)** → Maximal group where every node can reach every other node.

Study SCC algorithms separately at advanced graph level.

#### 9. Common Interview Patterns — Must Know

1. **Number of Islands** → Count components in a grid.
2. **Number of Provinces** → Count connected groups.
3. **Connected Components** → DFS/BFS or Union-Find.
4. **Network Connectivity** → Determine whether all nodes are connected.

#### 10. Key Points — Must Know

1. Connected → all vertices are reachable from each other.
2. Disconnected → graph contains separate groups.
3. Each separate group is a **connected component**.
4. An isolated vertex counts as **one component**.
5. To process a disconnected graph, run **DFS/BFS from every unvisited vertex**.
6. Connected components → think **DFS, BFS, or Union-Find**.
7. Standard traversal complexity → `O(V + E)`.