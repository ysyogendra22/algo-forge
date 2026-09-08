# BFS — Breadth First Search

#### 1. Definition — Must Know

1. **BFS** explores a graph **level by level**.
2. It visits all immediate neighbors before moving deeper.
3. BFS uses a **Queue (FIFO)**.
4. Use `visited` to prevent processing nodes repeatedly.

#### 2. How It Works — Must Know

Graph:

```text
    0
   / \
  1   2
 / \
3   4
```

BFS from `0`:

```text
0 → 1 → 2 → 3 → 4
```

Flow:

```text
Visit 0
  ↓
Visit 1, 2
  ↓
Visit 3, 4
```

Think:

```text
Level 0 → 0
Level 1 → 1, 2
Level 2 → 3, 4
```

#### 3. Core Logic — Must Know

```text
BFS(start):

1. Add start to Queue.
2. Mark start as visited.
3. While Queue is not empty:
   - Remove front node.
   - Process it.
   - Add all unvisited neighbors.
   - Mark them visited.
```

Core pattern:

```text
Queue → Remove Front → Visit Neighbors → Add Back
```

#### 4. Kotlin Implementation — Must Know

```kotlin
fun bfs(
    start: Int,
    graph: Array<MutableList<Int>>
) {
    val visited = BooleanArray(graph.size)
    val queue = ArrayDeque<Int>()

    queue.addLast(start)
    visited[start] = true

    while (queue.isNotEmpty()) {
        val node = queue.removeFirst()

        println(node)

        for (neighbor in graph[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true
                queue.addLast(neighbor)
            }
        }
    }
}
```

#### 5. Why Mark Visited Before Enqueue? — Must Know

Prefer:

```kotlin
visited[neighbor] = true
queue.addLast(neighbor)
```

Not after removing it from the queue.

Otherwise, the same node can be added multiple times by different neighbors.

#### 6. Level-by-Level BFS — Must Know

When the problem requires processing each level separately:

```kotlin
while (queue.isNotEmpty()) {

    val levelSize = queue.size

    repeat(levelSize) {
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

`levelSize` represents the number of nodes in the **current level**.

Useful for:

1. Minimum steps.
2. Distance from source.
3. Level-based processing.

#### 7. Shortest Path — Must Know

BFS finds the shortest path in an **unweighted graph**.

Example:

```text
A ----- B ----- D
 \             /
  ----- C ----
```

BFS explores:

```text
Distance 0 → A
Distance 1 → B, C
Distance 2 → D
```

The first time BFS reaches a node gives its minimum number of edges from the source.

#### 8. Distance Using BFS — Must Know

```kotlin
fun shortestDistance(
    start: Int,
    graph: Array<MutableList<Int>>
): IntArray {

    val distance = IntArray(graph.size) { -1 }
    val queue = ArrayDeque<Int>()

    queue.addLast(start)
    distance[start] = 0

    while (queue.isNotEmpty()) {
        val node = queue.removeFirst()

        for (neighbor in graph[node]) {
            if (distance[neighbor] == -1) {
                distance[neighbor] = distance[node] + 1
                queue.addLast(neighbor)
            }
        }
    }

    return distance
}
```

Here `distance != -1` also acts as the `visited` check.

#### 9. Disconnected Graph — Must Know

One BFS only visits nodes reachable from the starting node.

```text
0 --- 1       2 --- 3
```

To visit the entire graph:

```kotlin
for (node in graph.indices) {
    if (!visited[node]) {
        // Run BFS from node
    }
}
```

Same concept as DFS.

#### 10. Time & Space Complexity — Must Know

Using adjacency list:

```text
Time  → O(V + E)
Space → O(V)
```

1. Each vertex is visited once.
2. Each edge is examined during traversal.
3. Queue + visited can require `O(V)` space.

#### 11. Common BFS Patterns — Must Know

1. **Graph Traversal**
   ```text
   Queue + visited
   ```

2. **Shortest Path — Unweighted Graph**
   ```text
   BFS + distance
   ```

3. **Level / Minimum Steps**
   ```text
   Level-by-level BFS
   ```

4. **Connected Components**
   ```text
   BFS from every unvisited node
   ```

5. **Grid BFS**
   ```text
   Explore neighboring cells
   ```

6. **Multi-Source BFS — Good to Know**
   ```text
   Add multiple starting nodes to Queue initially
   ```

Common for problems where something spreads simultaneously from multiple locations.

#### 12. Common Interview Problems

1. Shortest Path in Unweighted Graph.
2. Number of Islands.
3. Rotting Oranges.
4. Word Ladder.
5. Minimum steps in a grid.
6. Graph connectivity / components.

#### 13. BFS vs DFS — Must Know

```text
BFS                         DFS

Queue                       Stack / Recursion
Level-by-level              Goes deep first
Shortest unweighted path    Path exploration
Minimum steps               Backtracking
O(V + E)                    O(V + E)
```

Use:

```text
Shortest / Minimum / Nearest → Think BFS

Explore / Components / Cycle → Often DFS
```

This is a guideline, not a strict rule.

#### 14. Edge Cases / Common Mistakes

1. Forgetting `visited` can cause infinite processing with cycles.
2. Prefer marking visited **when adding to the queue**.
3. One BFS does not cover a disconnected graph.
4. BFS does **not** solve general weighted shortest-path problems.
5. Traversal order depends on adjacency-list order.
6. Check empty graph / invalid starting node when required.

#### 15. Interview Must Remember

1. BFS = **level-by-level traversal**.
2. BFS uses a **Queue (FIFO)**.
3. Mark nodes visited when **enqueuing**.
4. Complexity → `O(V + E)`.
5. **Unweighted shortest path → BFS**.
6. Minimum steps / nearest / level problems → strongly consider BFS.
7. Multiple starting points → think **Multi-Source BFS**.