# Dependency Graph Problems

#### 1. Definition — Must Know

1. A **Dependency Graph** represents relationships where one task/item depends on another.
2. Usually modeled as a **Directed Graph**.
3. An edge:

```text id="dg01"
A → B
```

usually means:

```text id="dg02"
A must happen before B
```

4. Dependency problems commonly use **Topological Sort** and **Cycle Detection**.

#### 2. Common Examples — Must Know

Dependency graphs appear in:

```text id="dg03"
Course Prerequisites
Task Scheduling
Build Systems
Package Dependencies
Job Pipelines
Deployment Order
```

Example:

```text id="dg04"
Design → Develop → Test → Deploy
```

#### 3. Core Modeling — Must Know

Suppose:

```text id="dg05"
Course B requires Course A
```

Represent:

```text id="dg06"
A → B
```

Meaning:

```text id="dg07"
Complete A before B
```

The most important step is getting the **edge direction correct**.

#### 4. DAG Connection — Must Know

A valid dependency structure normally forms a:

```text id="dg08"
Directed Acyclic Graph
        ↓
       DAG
```

Why?

A cycle such as:

```text id="dg09"
A → B
↑   ↓
└── C
```

means:

```text id="dg10"
A depends on C
C depends on B
B depends on A
```

No task can be completed first.

Therefore:

```text id="dg11"
Cycle
  ↓
Invalid / Impossible Dependency Order
```

#### 5. Main Interview Questions — Must Know

Dependency graph problems usually ask:

```text id="dg12"
1. Can all tasks be completed?

2. What is a valid execution order?

3. Does a circular dependency exist?

4. Which tasks are ready now?
```

Map them to:

```text id="dg13"
Can complete?
     ↓
Cycle Detection


Find valid order?
     ↓
Topological Sort


Ready tasks?
     ↓
In-degree = 0
```

#### 6. Topological Sort — Must Know

For:

```text id="dg14"
A → B
A → C
B → D
C → D
```

Possible topological order:

```text id="dg15"
A → B → C → D
```

Another valid order:

```text id="dg16"
A → C → B → D
```

Topological order is **not necessarily unique**.

#### 7. Kahn's Algorithm Pattern — Must Know

Kahn's Algorithm is especially useful for dependency problems.

```text id="dg17"
1. Build adjacency list.

2. Calculate in-degree.

3. Add all in-degree 0 nodes to Queue.

4. Process them.

5. Reduce neighbors' in-degree.

6. When neighbor becomes 0:
      add it to Queue.

7. Count processed nodes.
```

Think:

```text id="dg18"
In-degree = Number of unfinished prerequisites
```

When:

```text id="dg19"
inDegree[node] == 0
```

the task is ready.

#### 8. Kotlin Implementation — Must Know

```kotlin id="dg20"
fun dependencyOrder(
    n: Int,
    dependencies: Array<IntArray>
): List<Int> {

    val graph = Array(n) {
        mutableListOf<Int>()
    }

    val indegree = IntArray(n)

    for (dependency in dependencies) {

        val prerequisite = dependency[0]
        val task = dependency[1]

        graph[prerequisite].add(task)
        indegree[task]++
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
        emptyList()
    }
}
```

#### 9. Cycle Detection — Must Know

After Kahn's Algorithm:

```text id="dg21"
processed == V
```

means:

```text id="dg22"
No Cycle
Dependency order possible
```

But:

```text id="dg23"
processed < V
```

means:

```text id="dg24"
Cycle Exists
Dependency order impossible
```

Why?

Nodes inside a cycle never reach:

```text id="dg25"
inDegree = 0
```

#### 10. Course Schedule Pattern — Must Know

Classic example:

```text id="dg26"
Course 1 requires Course 0

0 → 1
```

Question:

```text id="dg27"
Can I finish all courses?
```

Solve using:

```text id="dg28"
Cycle Detection
        ↓
Kahn's Algorithm
or
DFS State
```

If all nodes are processed:

```text id="dg29"
true
```

Otherwise:

```text id="dg30"
false
```

#### 11. DFS Alternative — Good to Know

Dependency cycles can also be detected using DFS states:

```text id="dg31"
0 → Unvisited
1 → Visiting
2 → Completed
```

If DFS reaches:

```text id="dg32"
Visiting → Visiting
```

there is a cycle.

```text id="dg33"
DFS + State
     ↓
Cycle Detection
```

For dependency ordering, Kahn's Algorithm is often easier to reason about.

#### 12. Time & Space Complexity — Must Know

Building graph:

```text id="dg34"
O(V + E)
```

Topological Sort:

```text id="dg35"
Time  → O(V + E)
Space → O(V + E)
```

Extra algorithmic space:

```text id="dg36"
In-degree → O(V)
Queue     → O(V)
Result    → O(V)
```

#### 13. Common Interview Patterns — Must Know

1. **Course prerequisites**
   ```text
   Topological Sort
   ```

2. **Task execution order**
   ```text
   Topological Sort
   ```

3. **Circular dependency**
   ```text
   Cycle Detection
   ```

4. **Build/package dependencies**
   ```text
   Directed Graph + Topological Sort
   ```

5. **Can all jobs complete?**
   ```text
   processed == V
   ```

6. **Currently executable tasks**
   ```text
   inDegree == 0
   ```

#### 14. Common Edge Cases — Must Know

1. No dependencies.
2. Single task.
3. Multiple independent dependency chains.
4. Circular dependency.
5. Self-dependency:

```text id="dg37"
A → A
```

6. Multiple valid execution orders.
7. Disconnected components.

Example:

```text id="dg38"
A → B

C → D
```

Both chains still belong to the dependency graph.

#### 15. Common Mistakes — Must Know

1. Reversing the dependency edge.

If:

```text id="dg39"
B depends on A
```

usually build:

```text id="dg40"
A → B
```

2. Calculating in-degree for the wrong node.
3. Assuming there is only one valid topological order.
4. Forgetting cycle detection.
5. Using normal BFS without tracking in-degree.
6. Assuming a dependency graph is always connected.
7. Forgetting a self-dependency is a cycle.

#### 16. Interview Must Remember

1. Dependency problems → usually **Directed Graph**.
2. Valid dependency ordering → **DAG**.
3. `A → B` → A must happen before B.
4. Ordering → **Topological Sort**.
5. Circular dependency → **Cycle Detection**.
6. Kahn's Algorithm uses **In-degree + Queue**.
7. `inDegree == 0` → task has no remaining prerequisites.
8. `processed < V` → **cycle exists**.
9. Complexity → **`O(V + E)`**.