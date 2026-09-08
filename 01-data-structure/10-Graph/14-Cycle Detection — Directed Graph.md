# Cycle Detection — Directed Graph

#### 1. Definition — Must Know

1. A cycle exists when following **directed edges** eventually leads back to a node in the same path.
2. Common approaches:
   - **DFS + Recursion Path / State** — Must Know.
   - **Topological Sort (Kahn's Algorithm)** — Must Know.

#### 2. Example — Must Know

Cyclic:

```text
0 → 1 → 2
    ↑   ↓
    └── 3
```

Cycle:

```text
1 → 2 → 3 → 1
```

Acyclic:

```text
0 → 1 → 2 → 3
```

No cycle exists.

#### 3. Why `visited` Alone Is Not Enough — Must Know

Consider:

```text
0 → 1
 \→ 2
    ↑
    1
```

`2` may already be visited when reached again.

But that does **not automatically mean a cycle**.

A cycle exists only when we reach a node that is already part of the **current DFS path**.

Think:

```text
Visited before        → Not necessarily cycle

In current DFS path   → Cycle
```

#### 4. DFS State Concept — Must Know

Use two arrays:

```text
visited[node]
path[node]
```

Meaning:

```text
visited → Node has been explored before.

path    → Node currently exists in this DFS recursion path.
```

Rule:

```text
neighbor is already in current path
              ↓
            Cycle
```

#### 5. Core DFS Logic — Must Know

```text
DFS(node):

1. Mark visited[node] = true
2. Mark path[node] = true

3. For every neighbor:

   if neighbor not visited:
       if DFS(neighbor):
           return true

   else if path[neighbor]:
       return true

4. Remove node from current path:
   path[node] = false

5. return false
```

#### 6. Kotlin Implementation — Must Know

```kotlin
fun hasCycle(
    n: Int,
    graph: Array<MutableList<Int>>
): Boolean {

    val visited = BooleanArray(n)
    val path = BooleanArray(n)

    fun dfs(node: Int): Boolean {

        visited[node] = true
        path[node] = true

        for (neighbor in graph[node]) {

            if (!visited[neighbor]) {

                if (dfs(neighbor)) {
                    return true
                }

            } else if (path[neighbor]) {

                return true
            }
        }

        path[node] = false

        return false
    }

    for (node in 0 until n) {

        if (!visited[node]) {
            if (dfs(node)) {
                return true
            }
        }
    }

    return false
}
```

#### 7. 3-State Approach — Good to Know

Instead of two arrays, use one state array:

```text
0 → Unvisited
1 → Visiting
2 → Visited / Completed
```

Cycle rule:

```text
Edge to state 1
      ↓
    Cycle
```

Kotlin idea:

```kotlin
val state = IntArray(n)

fun dfs(node: Int): Boolean {

    state[node] = 1

    for (neighbor in graph[node]) {

        if (state[neighbor] == 1) {
            return true
        }

        if (state[neighbor] == 0 && dfs(neighbor)) {
            return true
        }
    }

    state[node] = 2

    return false
}
```

This is a clean interview-friendly alternative.

#### 8. Why Remove Node from Current Path? — Must Know

After DFS finishes:

```kotlin
path[node] = false
```

because the node is no longer part of the **active recursion path**.

It remains:

```text
visited = true
path    = false
```

This distinction is critical.

#### 9. Kahn's Algorithm Approach — Must Know

Cycle detection can also use **Topological Sort**.

Logic:

```text
1. Calculate in-degree of every node.
2. Add all nodes with in-degree 0 to queue.
3. Process them and reduce neighbors' in-degree.
4. Count processed nodes.
```

Then:

```text
processedNodes == V
        ↓
     No Cycle

processedNodes < V
        ↓
       Cycle
```

Why?

Nodes inside a directed cycle can never all reach `in-degree = 0`.

Study the implementation under **Topological Sort / Kahn's Algorithm**.

#### 10. Complexity — Must Know

For DFS or Kahn's Algorithm:

```text
Time  → O(V + E)
Space → O(V)
```

Every vertex and edge is processed a constant number of times.

#### 11. Common Interview Patterns — Must Know

1. **Course Schedule**
   ```text
   Dependencies + Cycle Detection
   ```

2. **Task Dependencies**
   ```text
   Directed Graph + Cycle
   ```

3. **Can all tasks be completed?**
   ```text
   Detect cycle / Topological Sort
   ```

4. **Dependency ordering**
   ```text
   DAG + Topological Sort
   ```

#### 12. Undirected vs Directed Cycle Detection — Must Know

```text
Undirected                  Directed

DFS + Parent                DFS + Current Path
Visited neighbor            Node in active path
!= parent → Cycle           → Cycle

Alternative: Union-Find     Alternative: Kahn's
```

#### 13. Common Mistakes — Must Know

1. Treating every edge to a visited node as a cycle.
2. Forgetting `path[node] = false` after DFS completes.
3. Using undirected `parent` logic for directed graphs.
4. Running DFS from only one node in a disconnected graph.
5. Confusing `visited` with **currently visiting**.
6. Forgetting that a self-loop `A → A` is a cycle.

#### 14. Interview Must Remember

1. Directed cycle → think **current DFS path**.
2. `visited` alone is not enough.
3. `path[neighbor] == true` → cycle.
4. Clean alternative → `0 = unvisited, 1 = visiting, 2 = completed`.
5. **Kahn's Algorithm:** processed nodes `< V` → cycle.
6. Complexity → `O(V + E)`.
7. Dependency / Course Schedule problems → think **cycle detection + topological sort**.