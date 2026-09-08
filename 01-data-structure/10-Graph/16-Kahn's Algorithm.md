# Kahn's Algorithm

#### 1. Definition — Must Know

1. **Kahn's Algorithm** is a BFS-based algorithm for **Topological Sort**.
2. It repeatedly processes vertices with **in-degree = 0**.
3. Works on directed graphs.
4. A complete topological ordering exists only when the graph is a **DAG**.

#### 2. Core Concept — Must Know

**In-degree** = Number of incoming edges.

```text id="kahn01"
A → C ← B
    ↓
    D
```

```text id="kahn02"
A → 0
B → 0
C → 2
D → 1
```

Nodes with:

```text id="kahn03"
in-degree = 0
```

have no remaining dependencies and can be processed.

#### 3. How It Works — Must Know

For:

```text id="kahn04"
A → C
B → C
C → D
```

Initial:

```text id="kahn05"
A = 0
B = 0
C = 2
D = 1
```

Queue:

```text id="kahn06"
[A, B]
```

Process `A`:

```text id="kahn07"
C: 2 → 1
```

Process `B`:

```text id="kahn08"
C: 1 → 0

Queue → [C]
```

Process `C`:

```text id="kahn09"
D: 1 → 0

Queue → [D]
```

Result:

```text id="kahn10"
A → B → C → D
```

`B → A → C → D` would also be valid.

#### 4. Algorithm / Logic — Must Know

```text id="kahn11"
1. Calculate in-degree of every vertex.

2. Add all vertices with in-degree 0 to Queue.

3. While Queue is not empty:

   node = remove front

   add node to result

   for every neighbor:
       indegree[neighbor]--

       if indegree[neighbor] == 0:
           add neighbor to Queue

4. Check how many vertices were processed.
```

Think:

```text id="kahn12"
In-degree 0
    ↓
Queue
    ↓
Process Node
    ↓
Remove Dependencies
    ↓
New In-degree 0 Nodes
```

#### 5. Kotlin Implementation — Must Know

```kotlin id="kahn13"
fun kahn(
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

#### 6. Cycle Detection — Must Know

Consider:

```text id="kahn14"
A → B
↑   ↓
└── C
```

In-degree:

```text id="kahn15"
A = 1
B = 1
C = 1
```

There is no node with:

```text id="kahn16"
in-degree = 0
```

So nothing can be processed.

Rule:

```text id="kahn17"
Processed Nodes == V
        ↓
     No Cycle

Processed Nodes < V
        ↓
      Cycle
```

Kotlin:

```kotlin id="kahn18"
val hasCycle = result.size != n
```

#### 7. Why Cycle Detection Works — Must Know

In a cycle:

```text id="kahn19"
A → B → C → A
```

every node depends on another node inside the cycle.

Therefore, those dependencies can never be completely removed.

Their in-degree never reaches `0`.

#### 8. Time & Space Complexity — Must Know

```text id="kahn20"
Time  → O(V + E)
Space → O(V)
```

1. Calculate in-degree → `O(V + E)`.
2. Each vertex enters the queue at most once.
3. Each edge is processed once.
4. Queue + in-degree array → `O(V)` extra space.

#### 9. Common Interview Patterns — Must Know

1. **Dependency Ordering**
   ```text
   Topological Sort
   ```

2. **Course Schedule**
   ```text
   Can all courses be completed?
   ```

3. **Course Ordering**
   ```text
   Return valid order
   ```

4. **Task / Build Dependencies**
   ```text
   Determine execution order
   ```

5. **Directed Cycle Detection**
   ```text
   processed < V
   ```

#### 10. Common Mistakes — Must Know

1. Calculating in-degree in the wrong direction.
2. Forgetting to add **all** initial `in-degree = 0` nodes.
3. Forgetting to decrease neighbors' in-degree.
4. Adding a neighbor before its in-degree becomes `0`.
5. Assuming the topological order is unique.
6. Forgetting `result.size != n` cycle check.
7. Using Kahn's Algorithm directly for undirected graphs.

#### 11. Kahn's vs Normal BFS — Must Know

Normal BFS:

```text id="kahn21"
Start Node
    ↓
Visit Neighbors
```

Kahn's:

```text id="kahn22"
All In-degree 0 Nodes
        ↓
Process Dependencies
        ↓
Create New In-degree 0 Nodes
```

So Kahn's is **BFS driven by dependency counts**, not by distance from a source.

#### 12. Interview Must Remember

1. Kahn's = **BFS Topological Sort**.
2. Main tools → **In-degree + Queue**.
3. Start with **all `in-degree = 0` nodes**.
4. Processing a node removes its outgoing dependency edges.
5. Neighbor reaching `in-degree = 0` → add to queue.
6. `processed < V` → **directed cycle exists**.
7. Complexity → `O(V + E)`.