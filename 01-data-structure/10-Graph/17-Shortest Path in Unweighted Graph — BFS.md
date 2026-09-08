# Shortest Path in Unweighted Graph — BFS

#### 1. Definition — Must Know

1. In an **unweighted graph**, BFS finds the shortest path from a source to other vertices.
2. Shortest path means the **minimum number of edges**.
3. BFS works because it explores nodes **level by level**.

#### 2. Why BFS Works — Must Know

Graph:

```text
    1
   / \
  2   3
  |   |
  4---5
```

Starting from `1`:

```text
Level 0 → 1
Level 1 → 2, 3
Level 2 → 4, 5
```

Therefore:

```text
Distance(1 → 1) = 0
Distance(1 → 2) = 1
Distance(1 → 3) = 1
Distance(1 → 4) = 2
```

The **first time BFS reaches a node**, it has found its shortest distance from the source.

#### 3. Core Logic — Must Know

```text
1. Set all distances = -1.

2. distance[source] = 0.

3. Add source to Queue.

4. While Queue is not empty:

   node = remove front

   for each neighbor:

       if neighbor is unvisited:

           distance[neighbor] =
               distance[node] + 1

           add neighbor to Queue
```

Core pattern:

```text
BFS + Distance Array
```

#### 4. Kotlin Implementation — Must Know

```kotlin
fun shortestDistance(
    n: Int,
    graph: Array<MutableList<Int>>,
    source: Int
): IntArray {

    val distance = IntArray(n) { -1 }
    val queue = ArrayDeque<Int>()

    distance[source] = 0
    queue.addLast(source)

    while (queue.isNotEmpty()) {

        val node = queue.removeFirst()

        for (neighbor in graph[node]) {

            if (distance[neighbor] == -1) {

                distance[neighbor] =
                    distance[node] + 1

                queue.addLast(neighbor)
            }
        }
    }

    return distance
}
```

Here:

```text
distance == -1 → Unvisited
```

So a separate `visited` array is unnecessary.

#### 5. Finding the Actual Path — Must Know

Distance tells us the shortest **length**.

To reconstruct the actual path, store each node's parent.

```kotlin
fun shortestPath(
    n: Int,
    graph: Array<MutableList<Int>>,
    source: Int,
    target: Int
): List<Int> {

    val parent = IntArray(n) { -1 }
    val visited = BooleanArray(n)
    val queue = ArrayDeque<Int>()

    queue.addLast(source)
    visited[source] = true

    while (queue.isNotEmpty()) {

        val node = queue.removeFirst()

        if (node == target) break

        for (neighbor in graph[node]) {

            if (!visited[neighbor]) {

                visited[neighbor] = true
                parent[neighbor] = node

                queue.addLast(neighbor)
            }
        }
    }

    if (!visited[target]) return emptyList()

    val path = mutableListOf<Int>()
    var current = target

    while (current != -1) {
        path.add(current)
        current = parent[current]
    }

    path.reverse()

    return path
}
```

Example:

```text
parent[4] = 2
parent[2] = 1
```

Reconstruct backwards:

```text
4 → 2 → 1
```

Reverse:

```text
1 → 2 → 4
```

#### 6. Time & Space Complexity — Must Know

Using adjacency list:

```text
Time  → O(V + E)
Space → O(V)
```

1. Every vertex is visited at most once.
2. Every edge is examined.
3. Queue + distance/parent arrays require `O(V)` extra space.

#### 7. Grid Connection — Must Know

A grid with equal-cost movement is also an **unweighted graph**.

```text
S . .
# # .
. . T
```

Each cell:

```text
Cell → Vertex
Movement → Edge
```

Therefore:

```text
Minimum moves in grid
        ↓
       BFS
```

#### 8. Multi-Source BFS — Good to Know

If there are multiple starting points:

```text
S1 . . S2
```

Add all sources to the queue initially:

```text
Queue → [S1, S2]
```

Then run normal BFS.

Useful for:

1. Rotting Oranges.
2. Distance to nearest source.
3. Spread/infection problems.

#### 9. BFS vs Dijkstra — Must Know

```text
Unweighted / Equal-cost edges
            ↓
           BFS

Different non-negative weights
            ↓
         Dijkstra
```

Example:

```text
A --10-- B
 \       /
  1     1
   \   /
     C
```

BFS may prefer:

```text
A → B
```

because it has one edge.

But weighted shortest path is:

```text
A → C → B

Cost = 2
```

So normal BFS is not suitable for general weighted graphs.

#### 10. Common Interview Patterns — Must Know

1. **Minimum number of edges**
   ```text
   BFS
   ```

2. **Minimum moves / steps**
   ```text
   BFS
   ```

3. **Shortest path in grid**
   ```text
   BFS
   ```

4. **Nearest node / target**
   ```text
   BFS
   ```

5. **Multiple starting points**
   ```text
   Multi-Source BFS
   ```

#### 11. Common Mistakes — Must Know

1. Using DFS for shortest path in an unweighted graph.
2. Marking visited too late and adding the same node multiple times.
3. Using normal BFS when edges have different costs.
4. Forgetting unreachable nodes should remain `-1` or equivalent.
5. Storing only distance when the problem asks for the actual path.
6. Forgetting `parent` when path reconstruction is required.

#### 12. Interview Must Remember

1. **Unweighted shortest path → BFS**.
2. BFS explores nodes in increasing distance from the source.
3. `distance[neighbor] = distance[node] + 1`.
4. First visit gives the shortest distance.
5. Need actual path → maintain a **parent array**.
6. Multiple sources → initialize queue with **all sources**.
7. Complexity → `O(V + E)`.