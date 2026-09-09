# Dijkstra's Algorithm

#### 1. Definition — Must Know

1. **Dijkstra's Algorithm** finds the shortest distance from one source to all other vertices.
2. Used for **weighted graphs with non-negative edge weights**.
3. Uses a **Min Priority Queue / Min-Heap**.
4. It can work on directed or undirected graphs.

```text id="dij001"
Weighted + Non-negative edges
            ↓
         Dijkstra
```

#### 2. Why It Is Used — Must Know

BFS works when all edges have equal cost.

Dijkstra is needed when costs differ.

```text id="dij002"
A --10-- B
 \      /
  2    3
   \  /
    C
```

Paths from `A` to `B`:

```text id="dij003"
A → B       = 10

A → C → B   = 2 + 3 = 5
```

Shortest distance:

```text id="dij004"
5
```

#### 3. Core Concept — Relaxation — Must Know

The most important operation is **relaxation**.

For an edge:

```text id="dij005"
u --weight--> v
```

Check:

```text id="dij006"
distance[u] + weight < distance[v]
```

If true:

```text id="dij007"
distance[v] = distance[u] + weight
```

Example:

```text id="dij008"
distance[A] = 2

A --3--> B

Current distance[B] = 10
```

New possible distance:

```text id="dij009"
2 + 3 = 5
```

Since:

```text id="dij010"
5 < 10
```

update:

```text id="dij011"
distance[B] = 5
```

#### 4. How It Works — Must Know

```text id="dij012"
1. Set all distances = Infinity.

2. distance[source] = 0.

3. Add source to Min-Heap.

4. Remove node with smallest distance.

5. For every neighbor:
      newDistance = currentDistance + weight

      if newDistance < distance[neighbor]:
          update distance
          add updated pair to Min-Heap

6. Continue until heap is empty.
```

Core pattern:

```text id="dij013"
Min-Heap
   ↓
Smallest Distance
   ↓
Relax Neighbors
   ↓
Push Better Distances
```

#### 5. Graph Representation — Must Know

Weighted adjacency list:

```kotlin id="dij014"
data class Edge(
    val to: Int,
    val weight: Int
)

val graph = Array(n) {
    mutableListOf<Edge>()
}
```

For undirected graph:

```kotlin id="dij015"
graph[u].add(Edge(v, weight))
graph[v].add(Edge(u, weight))
```

For directed graph:

```kotlin id="dij016"
graph[u].add(Edge(v, weight))
```

#### 6. Kotlin Implementation — Must Know

```kotlin id="dij017"
import java.util.PriorityQueue

data class Edge(
    val to: Int,
    val weight: Int
)

data class State(
    val node: Int,
    val distance: Int
)

fun dijkstra(
    n: Int,
    graph: Array<MutableList<Edge>>,
    source: Int
): IntArray {

    val distance = IntArray(n) { Int.MAX_VALUE }

    val pq = PriorityQueue<State>(
        compareBy { it.distance }
    )

    distance[source] = 0
    pq.offer(State(source, 0))

    while (pq.isNotEmpty()) {

        val current = pq.poll()

        val node = current.node
        val currentDistance = current.distance

        if (currentDistance > distance[node]) {
            continue
        }

        for (edge in graph[node]) {

            val newDistance =
                currentDistance + edge.weight

            if (newDistance < distance[edge.to]) {

                distance[edge.to] = newDistance

                pq.offer(
                    State(edge.to, newDistance)
                )
            }
        }
    }

    return distance
}
```

#### 7. Why Skip Stale Entries? — Must Know

Java/Kotlin `PriorityQueue` does not conveniently decrease an existing key.

So the same node may enter the heap multiple times.

Example:

```text id="dij018"
(node=3, distance=10)
(node=3, distance=5)
```

When `10` is later removed:

```kotlin id="dij019"
if (currentDistance > distance[node]) {
    continue
}
```

because a better path (`5`) is already known.

#### 8. Shortest Path Reconstruction — Good to Know

If the actual path is required, maintain:

```kotlin id="dij020"
val parent = IntArray(n) { -1 }
```

During relaxation:

```kotlin id="dij021"
if (newDistance < distance[edge.to]) {

    distance[edge.to] = newDistance
    parent[edge.to] = node

    pq.offer(State(edge.to, newDistance))
}
```

Then reconstruct:

```text id="dij022"
Target → Parent → Parent → Source
```

and reverse it.

Same idea as BFS path reconstruction.

#### 9. Complexity — Must Know

Using:

```text id="dij023"
Adjacency List + Priority Queue
```

Typical complexity:

```text id="dij024"
Time  → O((V + E) log V)
Space → O(V + E)
```

Often simplified for connected graphs as:

```text id="dij025"
O(E log V)
```

Extra algorithmic space is mainly the distance array and priority queue.

#### 10. Why Dijkstra Fails with Negative Weights — Must Know

Example:

```text id="dij026"
A --5--> B
 \       ↑
  2     -10
   \     |
      → C
```

Negative edges can later produce a much cheaper path that breaks Dijkstra's greedy assumption.

Therefore:

```text id="dij027"
Non-negative weights
        ↓
     Dijkstra

Negative weights
        ↓
   Bellman-Ford
```

#### 11. BFS vs Dijkstra — Must Know

```text id="dij028"
BFS                         Dijkstra

Unweighted / equal cost     Weighted graph
Queue                       Min-Heap
Distance + 1                Distance + weight
O(V + E)                    O((V+E) log V)
```

Think:

```text id="dij029"
All edges same cost → BFS

Different non-negative costs → Dijkstra
```

#### 12. Common Interview Patterns — Must Know

1. **Shortest weighted path**
   ```text
   Dijkstra
   ```

2. **Minimum travel cost/time**
   ```text
   Dijkstra
   ```

3. **Network delay**
   ```text
   Dijkstra
   ```

4. **Weighted grid**
   ```text
   Dijkstra
   ```

5. **Actual shortest route**
   ```text
   Dijkstra + Parent
   ```

#### 13. Common Mistakes — Must Know

1. Using Dijkstra with negative edge weights.
2. Using normal Queue instead of Min-Heap.
3. Ordering PriorityQueue by node instead of distance.
4. Forgetting the relaxation condition.
5. Forgetting to skip stale heap entries.
6. Forgetting reverse edges when the graph is undirected.
7. Treating `Int.MAX_VALUE` as a normal distance and causing overflow in modified implementations.

#### 14. Interview Must Remember

1. Dijkstra → **weighted shortest path**.
2. Edge weights must be **non-negative**.
3. Main tools → **Adjacency List + Min-Heap + Distance Array**.
4. Core operation → **Relaxation**.
5. Always process the currently **smallest known distance**.
6. Skip stale PriorityQueue entries.
7. Complexity → approximately `O((V + E) log V)`.