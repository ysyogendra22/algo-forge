# Topological Sort

#### 1. Definition — Must Know

1. **Topological Sort** gives a linear ordering of vertices based on dependencies.
2. For every directed edge:

```text
A → B
```

`A` must appear **before** `B`.

3. Topological Sort works only on a:

```text
DAG = Directed Acyclic Graph
```

#### 2. Why It Is Used — Must Know

Used when something must happen **before something else**.

Examples:

1. Course prerequisites.
2. Task scheduling.
3. Build dependencies.
4. Package dependencies.
5. Workflow execution.

Think:

```text
Dependencies + Ordering
        ↓
Topological Sort
```

#### 3. Example — Must Know

Dependencies:

```text
A → C
B → C
C → D
```

Valid topological orders:

```text
A → B → C → D
```

or:

```text
B → A → C → D
```

Topological order is **not necessarily unique**.

But `C` must appear after `A` and `B`.

#### 4. Two Main Approaches — Must Know

1. **Kahn's Algorithm**
   - BFS.
   - Uses **In-degree + Queue**.

2. **DFS Topological Sort**
   - Uses DFS.
   - Add node after processing all dependencies.
   - Reverse the result.

For interviews, know both, but **Kahn's Algorithm is especially useful because cycle detection is straightforward**.

---

#### 5. Kahn's Algorithm — Must Know

In-degree:

```text
Number of incoming edges
```

Example:

```text
A → C ← B
    ↓
    D
```

```text
A → 0
B → 0
C → 2
D → 1
```

Start with nodes having:

```text
in-degree = 0
```

because they have no remaining prerequisites.

#### 6. Kahn's Algorithm Logic — Must Know

```text
1. Calculate in-degree of every node.

2. Add all nodes with in-degree 0 to Queue.

3. While Queue is not empty:

   Remove node.

   Add node to result.

   For every neighbor:
       decrease in-degree.

       if in-degree becomes 0:
           add neighbor to Queue.

4. Return result.
```

Core pattern:

```text
In-degree 0
     ↓
Process
     ↓
Remove its dependency edges
     ↓
New in-degree 0 nodes
```

#### 7. Kotlin — Kahn's Algorithm

```kotlin
fun topologicalSort(
    n: Int,
    graph: Array<MutableList<Int>>
): List<Int> {

    val indegree = IntArray(n)

    for (node in 0 until n) {
        for (neighbor in graph[node]) {
            indegree[neighbor]++
        }
    }

    val queue = ArrayDeque<Int>()

    for (node in 0 until n) {
        if (indegree[node] == 0) {
            queue.addLast(node)
        }
    }

    val result = mutableListOf<Int>()

    while (queue.isNotEmpty()) {

        val node = queue.removeFirst()
        result.add(node)

        for (neighbor in graph[node]) {

            indegree[neighbor]--

            if (indegree[neighbor] == 0) {
                queue.addLast(neighbor)
            }
        }
    }

    return result
}
```

#### 8. Cycle Detection with Kahn's — Must Know

If the graph contains a cycle:

```text
A → B
↑   ↓
└── C
```

nodes in the cycle cannot all become `in-degree = 0`.

Therefore:

```text
result.size == V
      ↓
Valid Topological Order

result.size < V
      ↓
Cycle Exists
```

Interview version:

```kotlin
if (result.size != n) {
    // Cycle exists
}
```

#### 9. DFS Topological Sort — Must Know

Core idea:

```text
Visit Node
   ↓
Visit all neighbors
   ↓
Add node after neighbors
   ↓
Reverse result
```

Why?

A node is added only after everything reachable from it has been processed.

#### 10. Kotlin — DFS Approach

```kotlin
fun topologicalSort(
    n: Int,
    graph: Array<MutableList<Int>>
): List<Int> {

    val visited = BooleanArray(n)
    val result = mutableListOf<Int>()

    fun dfs(node: Int) {

        visited[node] = true

        for (neighbor in graph[node]) {
            if (!visited[neighbor]) {
                dfs(neighbor)
            }
        }

        result.add(node)
    }

    for (node in 0 until n) {
        if (!visited[node]) {
            dfs(node)
        }
    }

    return result.reversed()
}
```

> This simple DFS version assumes the graph is already known to be a DAG. If cycles are possible, add DFS cycle-state detection.

#### 11. Time & Space Complexity — Must Know

Both approaches:

```text
Time  → O(V + E)
Space → O(V)
```

Excluding the graph storage itself.

#### 12. Common Interview Patterns — Must Know

1. **Course Schedule**
   ```text
   Can all courses be completed?
   ```

2. **Course Schedule II**
   ```text
   Return valid course order.
   ```

3. **Task Scheduling**
   ```text
   Dependency → execution order
   ```

4. **Build / Package Dependencies**
   ```text
   Dependency ordering
   ```

5. **Cycle Detection**
   ```text
   Kahn's processed count < V
   ```

#### 13. Common Mistakes — Must Know

1. Using Topological Sort on an **undirected graph**.
2. Forgetting that the graph must be **acyclic** for a valid ordering.
3. Assuming the topological order is unique.
4. Building dependency edges in the wrong direction.
5. Forgetting to decrease neighbors' in-degree.
6. Returning Kahn's result without checking `result.size == V` when cycles are possible.

#### 14. Kahn's vs DFS — Must Know

```text
Kahn's Algorithm             DFS

BFS based                    DFS based
Uses Queue                   Uses recursion/stack
Uses In-degree               Uses postorder
Easy cycle detection         Needs DFS state for cycle
O(V + E)                     O(V + E)
```

#### 15. Interview Must Remember

1. Topological Sort → **dependency ordering**.
2. Works only for a **DAG**.
3. Edge `A → B` means `A` comes before `B`.
4. Kahn's → **In-degree + Queue**.
5. Kahn's: `processed < V` → **cycle exists**.
6. DFS → process neighbors first, then node, then reverse.
7. Topological ordering can have **multiple valid answers**.