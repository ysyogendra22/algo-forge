# Cycle Detection — Undirected Graph

#### 1. Definition — Must Know

1. A cycle exists when you can start from a vertex and return to it through a different path.
2. For an undirected graph, cycle detection commonly uses:
   - **DFS + Parent** — Must Know.
   - **BFS + Parent** — Good to Know.
   - **Union-Find** — Good to Know.

#### 2. Example — Must Know

Cyclic:

```text id="jygd4w"
0 ----- 1
|       |
2 ----- 3
```

Cycle:

```text id="aifmps"
0 → 1 → 3 → 2 → 0
```

Acyclic:

```text id="km08w7"
0 ----- 1
|
2 ----- 3
```

No cycle exists.

#### 3. Why `visited` Alone Is Not Enough — Must Know

Consider:

```text id="nv11vq"
0 ----- 1
```

DFS:

```text id="skmb4s"
0 → 1
```

From `1`, neighbor `0` is already visited.

But this is **not a cycle** because `0` is the node we came from.

Therefore track:

```text id="e2l5g3"
Current Node + Parent
```

Rule:

```text id="j4gdty"
Visited neighbor AND neighbor != parent
                ↓
             Cycle
```

#### 4. DFS Logic — Must Know

```text id="gk8t21"
DFS(node, parent):

1. Mark node visited.

2. For every neighbor:

   if neighbor not visited:
       if DFS(neighbor, node):
           return true

   else if neighbor != parent:
       return true

3. return false
```

Core pattern:

```text id="3o46x4"
Unvisited neighbor
      ↓
Continue DFS

Visited neighbor
      ↓
Is it parent?
  ↓          ↓
 Yes         No
 ↓           ↓
Ignore      Cycle
```

#### 5. Kotlin Implementation — Must Know

```kotlin id="kw4amq"
fun hasCycle(
    n: Int,
    graph: Array<MutableList<Int>>
): Boolean {

    val visited = BooleanArray(n)

    fun dfs(node: Int, parent: Int): Boolean {

        visited[node] = true

        for (neighbor in graph[node]) {

            if (!visited[neighbor]) {

                if (dfs(neighbor, node)) {
                    return true
                }

            } else if (neighbor != parent) {

                return true
            }
        }

        return false
    }

    for (node in 0 until n) {

        if (!visited[node]) {

            if (dfs(node, -1)) {
                return true
            }
        }
    }

    return false
}
```

#### 6. Why Loop Through Every Node? — Must Know

Graph may be disconnected:

```text id="79d23g"
0 --- 1       2 --- 3
              |     |
              5 --- 4
```

Starting DFS from `0` never reaches the second component.

Therefore:

```kotlin id="qutn3c"
for (node in 0 until n) {
    if (!visited[node]) {
        if (dfs(node, -1)) return true
    }
}
```

A cycle in **any component** means the graph contains a cycle.

#### 7. BFS + Parent — Good to Know

Store:

```text id="j9p1fb"
(node, parent)
```

Logic is the same:

```text id="94pg2p"
Visited neighbor != parent
          ↓
        Cycle
```

Example structure:

```kotlin id="wrb7a2"
data class State(
    val node: Int,
    val parent: Int
)
```

DFS is usually simpler to write in interviews.

#### 8. Union-Find Approach — Good to Know

Process each edge:

```text id="uxd1cb"
(u, v)
```

If:

```text id="35pdd4"
find(u) == find(v)
```

they are already connected.

Adding `(u, v)` creates a cycle.

Otherwise:

```text id="gmgw8s"
union(u, v)
```

Useful when the problem is naturally based on **processing edges / dynamic connectivity**.

#### 9. Time & Space Complexity — Must Know

DFS/BFS with adjacency list:

```text id="dm3xgm"
Time  → O(V + E)
Space → O(V)
```

1. Each vertex is visited once.
2. Each undirected edge appears in adjacency lists twice, but this is still `O(E)`.
3. `visited` + recursion/queue requires up to `O(V)` extra space.

#### 10. Common Mistakes — Must Know

1. Treating the parent edge as a cycle.
2. Using only `visited` without tracking parent.
3. Running DFS from only one vertex in a disconnected graph.
4. Forgetting to add both directions when building an undirected graph.
5. Confusing this logic with **directed graph cycle detection**.

#### 11. Directed vs Undirected — Must Know

```text id="8okvne"
Undirected:

DFS + visited + parent


Directed:

DFS + visited/current-path state
```

Do not use the undirected `parent` technique directly for directed graphs.

#### 12. Interview Must Remember

1. Undirected cycle detection → **DFS + Parent**.
2. `visited neighbor != parent` → **cycle**.
3. Parent itself is visited but does **not** indicate a cycle.
4. Check every component in a disconnected graph.
5. Complexity → `O(V + E)`.
6. BFS can use the same parent concept.
7. **Union-Find** is another important cycle-detection approach for undirected graphs.