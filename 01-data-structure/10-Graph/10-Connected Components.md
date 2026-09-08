# Connected Components

#### 1. Definition — Must Know

1. A **Connected Component** is a group of vertices where every vertex is reachable from the others.
2. A disconnected graph can contain multiple connected components.
3. An isolated vertex is also one component.

```text
0 --- 1       3 --- 4

     2

Components = 3

[0,1]
[2]
[3,4]
```

#### 2. Why It Is Used — Must Know

Used to identify separate groups inside a graph.

Examples:

1. Groups of connected users.
2. Separate computer networks.
3. Islands in a grid.
4. Network clusters.
5. Provinces/cities connectivity.

#### 3. Core Logic — Must Know

The main pattern:

```text
components = 0

For every vertex:

    if not visited:
        run DFS/BFS
        components++
```

Why?

1. One DFS/BFS visits the **entire component**.
2. Finding another unvisited node means we found a **new component**.

#### 4. DFS Implementation — Must Know

```kotlin
fun countComponents(
    n: Int,
    edges: Array<IntArray>
): Int {

    val graph = Array(n) { mutableListOf<Int>() }

    for ((u, v) in edges) {
        graph[u].add(v)
        graph[v].add(u)
    }

    val visited = BooleanArray(n)

    fun dfs(node: Int) {
        visited[node] = true

        for (neighbor in graph[node]) {
            if (!visited[neighbor]) {
                dfs(neighbor)
            }
        }
    }

    var components = 0

    for (node in 0 until n) {
        if (!visited[node]) {
            dfs(node)
            components++
        }
    }

    return components
}
```

#### 5. BFS Implementation — Good to Know

```kotlin
fun bfs(
    start: Int,
    graph: Array<MutableList<Int>>,
    visited: BooleanArray
) {
    val queue = ArrayDeque<Int>()

    queue.addLast(start)
    visited[start] = true

    while (queue.isNotEmpty()) {
        val node = queue.removeFirst()

        for (neighbor in graph[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true
                queue.addLast(neighbor)
            }
        }
    }
}
```

Then:

```kotlin
var components = 0

for (node in graph.indices) {
    if (!visited[node]) {
        bfs(node, graph, visited)
        components++
    }
}
```

#### 6. Time & Space Complexity — Must Know

With an adjacency list:

```text
Time  → O(V + E)
Space → O(V + E)
```

1. Building adjacency list → `O(V + E)` space.
2. Traversal → `O(V + E)`.
3. `visited` + DFS/BFS working space → `O(V)`.

If the graph is already provided as an adjacency list, **extra traversal space** is `O(V)`.

#### 7. Grid Connection — Must Know

Many grid problems are actually connected-component problems.

Example:

```text
1 1 0 0
1 0 0 1
0 0 1 1
```

Each connected group of `1`s can represent one component.

Pattern:

```text
Unvisited land
      ↓
Run DFS/BFS
      ↓
Mark entire island
      ↓
components++
```

This is the core idea behind **Number of Islands**.

#### 8. Union-Find — Good to Know

Connected components can also be solved using:

```text
Union-Find / Disjoint Set Union (DSU)
```

Useful when:

1. Edges are added dynamically.
2. You repeatedly need connectivity checks.
3. Problems are naturally based on merging groups.

Study DSU separately.

#### 9. Directed Graphs — Good to Know

Normal connected-component logic mainly applies to **undirected graphs**.

For directed graphs, you may encounter:

```text
Strongly Connected Components (SCC)
```

SCC requires different algorithms such as:

```text
Kosaraju
Tarjan
```

These are lower priority than basic connected components for initial interview preparation.

#### 10. Common Interview Problems — Must Know

1. Number of Connected Components.
2. Number of Islands.
3. Number of Provinces.
4. Network Connectivity.
5. Friend Circles / Groups.

The underlying pattern is usually:

```text
For each unvisited node → DFS/BFS → count++
```

#### 11. Common Mistakes — Must Know

1. Running DFS/BFS only once misses disconnected components.
2. Forgetting to mark nodes as visited.
3. Forgetting both directions when building an undirected graph.
4. Forgetting that an **isolated node counts as one component**.
5. In grid problems, check boundaries before visiting neighbors.

#### 12. Interview Must Remember

1. One **DFS/BFS = one complete component**.
2. Loop through **every vertex**.
3. Unvisited vertex → new component → `count++`.
4. Standard complexity → `O(V + E)`.
5. Isolated vertex → one component.
6. **DFS or BFS** both work.
7. Dynamic connectivity / repeated merging → think **Union-Find**.