# DAG Problems

#### 1. Definition — Must Know

1. **DAG = Directed Acyclic Graph**.
2. Edges have direction.
3. The graph contains **no directed cycle**.

```text id="dag01"
A → B → D
 \→ C →/
```

This is a DAG because no path returns to an earlier node.

#### 2. Why DAG Is Important — Must Know

DAGs naturally represent:

```text id="dag02"
Dependencies
Prerequisites
Task Scheduling
Build Systems
Workflows
Job Pipelines
```

Example:

```text id="dag03"
Design → Develop → Test → Deploy
```

#### 3. Core Property — Must Know

Every DAG has at least one valid:

```text id="dag04"
Topological Ordering
```

Example:

```text id="dag05"
A → B
A → C
B → D
C → D
```

Possible orders:

```text id="dag06"
A → B → C → D

A → C → B → D
```

Topological ordering may **not be unique**.

#### 4. How to Recognize DAG Problems — Must Know

Look for:

```text id="dag07"
Prerequisites
Dependencies
Before / After
Execution Order
Build Order
Task Scheduling
No Circular Dependency
```

Then think:

```text id="dag08"
Directed Graph
      ↓
Cycle Detection
      ↓
Topological Sort
```

#### 5. Topological Sort — Must Know

Two standard approaches:

```text id="dag09"
1. Kahn's Algorithm
   → BFS + In-degree

2. DFS
   → Postorder + Reverse
```

For dependency problems, Kahn's Algorithm is often the easiest approach.

#### 6. Kahn's Algorithm — Must Know

Core idea:

```text id="dag10"
In-degree = number of prerequisites
```

Steps:

```text id="dag11"
1. Calculate in-degree.

2. Add all in-degree 0 nodes to Queue.

3. Process a node.

4. Reduce neighbors' in-degree.

5. If neighbor becomes 0:
      add to Queue.

6. Continue until Queue is empty.
```

#### 7. Cycle Detection in DAG Problems — Must Know

If Kahn processes:

```text id="dag12"
processed == V
```

then:

```text id="dag13"
No Cycle
→ Graph is a DAG
```

If:

```text id="dag14"
processed < V
```

then:

```text id="dag15"
Cycle Exists
→ Not a DAG
```

Nodes inside a cycle never reach `inDegree = 0`.

#### 8. Kotlin — Check DAG + Topological Order

```kotlin id="dag16"
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

    val order = mutableListOf<Int>()

    while (queue.isNotEmpty()) {

        val node = queue.removeFirst()
        order.add(node)

        for (neighbor in graph[node]) {

            indegree[neighbor]--

            if (indegree[neighbor] == 0) {
                queue.addLast(neighbor)
            }
        }
    }

    return if (order.size == n) {
        order
    } else {
        emptyList() // Cycle exists
    }
}
```

#### 9. DFS DAG Pattern — Good to Know

DFS can also detect cycles using:

```text id="dag17"
0 → Unvisited
1 → Visiting
2 → Completed
```

If DFS finds an edge to:

```text id="dag18"
Visiting Node
```

then:

```text id="dag19"
Cycle Exists
→ Not DAG
```

If no cycle exists, reverse DFS postorder to get a topological order.

#### 10. Shortest Path in DAG — Good to Know

A DAG allows an efficient shortest-path approach:

```text id="dag20"
Topological Sort
      ↓
Process nodes in order
      ↓
Relax outgoing edges
```

Complexity:

```text id="dag21"
O(V + E)
```

Important advantage:

Unlike Dijkstra, DAG shortest path can handle **negative edge weights** because there are no cycles.

#### 11. DAG Shortest Path Logic

```text id="dag22"
1. Topologically sort graph.

2. distance[source] = 0.

3. Process vertices in topological order.

4. Relax outgoing edges.

5. Continue until all vertices processed.
```

Relaxation:

```text id="dag23"
newDistance =
    distance[u] + weight(u, v)
```

If smaller:

```text id="dag24"
distance[v] = newDistance
```

#### 12. Common DAG Patterns — Must Know

1. **Course prerequisites**
   ```text
   Topological Sort
   ```

2. **Task scheduling**
   ```text
   Topological Sort
   ```

3. **Can all tasks finish?**
   ```text
   Cycle Detection
   ```

4. **Build order**
   ```text
   Topological Sort
   ```

5. **Shortest path in DAG**
   ```text
   Topological Sort + Relaxation
   ```

6. **Dependency processing**
   ```text
   In-degree / Kahn
   ```

#### 13. DAG vs Tree — Good to Know

```text id="dag25"
Tree                         DAG

Usually hierarchical        Dependency structure

Unique parent except root   Node can have many parents

Connected                   May be disconnected

No cycles                   No directed cycles

V - 1 edges                 Can have many edges
```

A DAG is **not necessarily a tree**.

#### 14. Complexity — Must Know

Topological Sort:

```text id="dag26"
Time  → O(V + E)
Space → O(V)
```

excluding graph storage.

Including adjacency list:

```text id="dag27"
Space → O(V + E)
```

DAG shortest path:

```text id="dag28"
Time → O(V + E)
```

#### 15. Common Edge Cases — Must Know

1. Single node.
2. No edges.
3. Multiple source nodes (`inDegree = 0`).
4. Multiple valid topological orders.
5. Disconnected DAG.
6. Self-loop → not DAG.
7. Circular dependency → not DAG.

#### 16. Common Mistakes — Must Know

1. Thinking every directed graph is a DAG.
2. Forgetting to check for cycles.
3. Reversing dependency edge direction.
4. Assuming topological order is unique.
5. Trying Topological Sort on an undirected graph.
6. Assuming a DAG must be connected.
7. Assuming DAG shortest path requires Dijkstra.

#### 17. Interview Must Remember

1. **DAG = Directed + No Cycle**.
2. DAG always has a **Topological Ordering**.
3. Dependencies/prerequisites → think **DAG**.
4. Kahn → **In-degree + Queue**.
5. `processed < V` → cycle → **not a DAG**.
6. Multiple topological orders may exist.
7. DAG shortest path → **Topological Sort + Relaxation**.
8. Topological Sort complexity → **`O(V + E)`**.