# DFS — Depth First Search

#### 1. Definition — Must Know

1. **DFS** explores a graph by going as deep as possible before backtracking.
2. Implement using:
   - **Recursion** → most common in interviews.
   - **Stack** → iterative approach.
3. Use a `visited` structure to avoid revisiting nodes.

#### 2. How It Works — Must Know

Graph:

```text
0 ----- 1
|       |
2 ----- 3
```

Starting from `0`, one possible DFS:

```text
0 → 1 → 3 → 2
```

Flow:

```text
Visit 0
  ↓
Visit 1
  ↓
Visit 3
  ↓
Visit 2
  ↓
No unvisited neighbor
  ↓
Backtrack
```

> DFS order can vary depending on adjacency-list order.

#### 3. Core Logic — Must Know

```text
DFS(node):

1. Mark node as visited.
2. Process node.
3. For every neighbor:
      if not visited:
          DFS(neighbor)
4. Backtrack.
```

The core pattern:

```text
Visit → Explore → Backtrack
```

#### 4. Recursive DFS — Must Know

Kotlin:

```kotlin
fun dfs(
    node: Int,
    graph: Array<MutableList<Int>>,
    visited: BooleanArray
) {
    visited[node] = true

    for (neighbor in graph[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, graph, visited)
        }
    }
}
```

Usage:

```kotlin
val graph = Array(4) { mutableListOf<Int>() }

graph[0].addAll(listOf(1, 2))
graph[1].addAll(listOf(0, 3))
graph[2].addAll(listOf(0, 3))
graph[3].addAll(listOf(1, 2))

val visited = BooleanArray(4)

dfs(0, graph, visited)
```

#### 5. Iterative DFS — Good to Know

Use an explicit **Stack**.

```kotlin
fun dfs(
    start: Int,
    graph: Array<MutableList<Int>>
) {
    val visited = BooleanArray(graph.size)
    val stack = ArrayDeque<Int>()

    stack.addLast(start)

    while (stack.isNotEmpty()) {
        val node = stack.removeLast()

        if (visited[node]) continue

        visited[node] = true

        for (neighbor in graph[node]) {
            if (!visited[neighbor]) {
                stack.addLast(neighbor)
            }
        }
    }
}
```

Recursive DFS uses the **call stack**; iterative DFS uses an **explicit stack**.

#### 6. Disconnected Graph — Must Know

Calling:

```kotlin
dfs(0, graph, visited)
```

only visits nodes reachable from `0`.

For a disconnected graph:

```text
0 --- 1       2 --- 3
```

Run DFS from every unvisited node:

```kotlin
for (node in graph.indices) {
    if (!visited[node]) {
        dfs(node, graph, visited)
    }
}
```

This pattern is commonly used for **connected-component counting**.

#### 7. Time & Space Complexity — Must Know

With an adjacency list:

```text
Time  → O(V + E)
Space → O(V)
```

1. Every vertex is visited once.
2. Every edge is examined during traversal.
3. `visited` requires `O(V)`.
4. Recursion/stack can require up to `O(V)`.

#### 8. Common DFS Patterns — Must Know

1. **Graph Traversal**
   ```text
   DFS + visited
   ```

2. **Connected Components**
   ```text
   For every unvisited node → DFS
   ```

3. **Cycle Detection**
   ```text
   Undirected → DFS + parent
   Directed   → DFS + recursion path/state
   ```

4. **Path / Reachability**
   ```text
   Can A reach B?
   ```

5. **Grid Problems**
   ```text
   DFS in 4/8 directions
   ```

6. **Backtracking**
   ```text
   Choose → Explore → Undo
   ```

#### 9. Common Interview Problems — Must Know

1. Number of Islands.
2. Number of Connected Components.
3. Clone Graph.
4. Detect Cycle.
5. Path Exists Between Two Nodes.
6. Flood Fill.

Focus on the **patterns**, not memorizing individual solutions.

#### 10. Edge Cases / Common Mistakes — Must Know

1. Forgetting `visited` can cause infinite traversal when cycles exist.
2. Mark a node visited **before recursively exploring its neighbors**.
3. One DFS does not necessarily cover a disconnected graph.
4. Recursive DFS can cause stack overflow on very deep graphs.
5. DFS traversal order is not guaranteed unless neighbor order is controlled.
6. Directed and undirected cycle detection require different logic.

#### 11. DFS vs BFS — Must Know

```text
DFS                         BFS

Uses Stack                  Uses Queue
Goes deep first             Goes level-by-level
Great for components        Great for shortest path
Great for cycle/path DFS    Great for minimum-edge distance
```

For an **unweighted shortest-path problem**, usually prefer BFS.

#### 12. Interview Must Remember

1. DFS → **go deep, then backtrack**.
2. Core tools → `visited + recursion/stack`.
3. Complexity → `O(V + E)`.
4. Disconnected graph → DFS from **every unvisited node**.
5. Always think about **cycles** before traversing a graph.
6. DFS is heavily used for **components, reachability, cycle detection, and grid problems**.
7. Recursive DFS is usually the simplest interview implementation.