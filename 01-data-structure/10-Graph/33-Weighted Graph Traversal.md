# Weighted Graph Traversal

#### 1. Definition — Must Know

1. A **Weighted Graph** has a value/cost associated with each edge.
2. Weight may represent:

```text id="wgt01"
Distance
Cost
Time
Risk
Latency
```

Example:

```text id="wgt02"
A --5-- B
|
2
|
C
```

#### 2. Graph Representation — Must Know

Weighted adjacency list:

```kotlin id="wgt03"
data class Edge(
    val to: Int,
    val weight: Int
)

val graph = Array(n) {
    mutableListOf<Edge>()
}
```

Undirected:

```kotlin id="wgt04"
graph[u].add(Edge(v, weight))
graph[v].add(Edge(u, weight))
```

Directed:

```kotlin id="wgt05"
graph[u].add(Edge(v, weight))
```

#### 3. Important Concept — Must Know

**Traversal** and **shortest path** are different.

If you only need to:

```text id="wgt06"
Visit / Explore all reachable nodes
```

you can still use:

```text id="wgt07"
DFS or BFS
```

The edge weight does not change basic traversal.

If you need:

```text id="wgt08"
Minimum Cost / Shortest Weighted Path
```

then the weights determine which algorithm to use.

#### 4. DFS on Weighted Graph — Must Know

DFS works normally; each neighbor also has a weight.

```kotlin id="wgt09"
fun dfs(
    node: Int,
    graph: Array<MutableList<Edge>>,
    visited: BooleanArray
) {

    visited[node] = true

    for (edge in graph[node]) {

        if (!visited[edge.to]) {
            dfs(edge.to, graph, visited)
        }
    }
}
```

If needed, you can access:

```kotlin id="wgt10"
edge.weight
```

during traversal.

#### 5. BFS on Weighted Graph — Must Know

BFS can also **traverse** a weighted graph:

```kotlin id="wgt11"
fun bfs(
    start: Int,
    graph: Array<MutableList<Edge>>
) {

    val visited = BooleanArray(graph.size)
    val queue = ArrayDeque<Int>()

    visited[start] = true
    queue.addLast(start)

    while (queue.isNotEmpty()) {

        val node = queue.removeFirst()

        for (edge in graph[node]) {

            if (!visited[edge.to]) {

                visited[edge.to] = true
                queue.addLast(edge.to)
            }
        }
    }
}
```

But normal BFS does **not** generally give the minimum weighted cost.

#### 6. Choosing the Correct Algorithm — Must Know

This is the most important part.

```text id="wgt12"
Unweighted / Equal Weight
        ↓
       BFS


Different Non-negative Weights
        ↓
     Dijkstra


Negative Edge Weights
        ↓
   Bellman-Ford


All-Pairs Shortest Path
        ↓
   Floyd-Warshall
```

For normal exploration:

```text id="wgt13"
DFS / BFS
```

#### 7. Why BFS Fails for Different Weights — Must Know

Example:

```text id="wgt14"
A --10-- B
 \      /
  2    3
   \  /
    C
```

BFS may see:

```text id="wgt15"
A → B
```

as one edge.

Cost:

```text id="wgt16"
10
```

But:

```text id="wgt17"
A → C → B
```

costs:

```text id="wgt18"
2 + 3 = 5
```

So:

```text id="wgt19"
Fewest Edges ≠ Minimum Weighted Cost
```

#### 8. Dijkstra Pattern — Must Know

For non-negative weighted shortest paths:

```text id="wgt20"
Adjacency List
      +
Distance Array
      +
Min-Heap
```

Relaxation:

```text id="wgt21"
newDistance =
    distance[current] + edge.weight
```

If:

```text id="wgt22"
newDistance < distance[neighbor]
```

update the neighbor's distance.

#### 9. Weight Types Matter — Must Know

Before choosing an algorithm, check the weights.

```text id="wgt23"
All weights equal
      ↓
     BFS


Weights 0 or 1
      ↓
   0-1 BFS


Non-negative weights
      ↓
   Dijkstra


Negative weights
      ↓
 Bellman-Ford
```

**0-1 BFS** is Good to Know for graphs where every edge weight is exactly `0` or `1`.

#### 10. Weighted Grid — Good to Know

A grid can also represent a weighted graph.

```text id="wgt24"
1  5  2
2  1  3
4  2  1
```

Each cell/move may have a cost.

If movement costs differ:

```text id="wgt25"
Normal BFS ❌

Dijkstra ✓
```

If every movement has the same cost:

```text id="wgt26"
BFS ✓
```

#### 11. Time & Space Complexity — Must Know

Basic BFS/DFS traversal:

```text id="wgt27"
Time  → O(V + E)
Space → O(V)
```

Dijkstra with adjacency list + Min-Heap:

```text id="wgt28"
Time → O((V + E) log V)
```

Graph storage:

```text id="wgt29"
O(V + E)
```

#### 12. Common Interview Patterns — Must Know

1. **Just visit weighted graph**
   ```text
   DFS / BFS
   ```

2. **Minimum travel time**
   ```text
   Dijkstra
   ```

3. **Minimum cost**
   ```text
   Dijkstra
   ```

4. **Equal-cost moves**
   ```text
   BFS
   ```

5. **0/1 edge costs**
   ```text
   0-1 BFS
   ```

6. **Negative weights**
   ```text
   Bellman-Ford
   ```

#### 13. Common Mistakes — Must Know

1. Assuming a weighted graph always requires Dijkstra.
2. Using BFS for shortest path when edge weights differ.
3. Confusing minimum number of edges with minimum total cost.
4. Using Dijkstra with negative weights.
5. Forgetting to store the weight in the adjacency list.
6. Adding reverse edges when the graph is directed.
7. Ignoring whether weights are equal, `0/1`, non-negative, or negative.

#### 14. Interview Must Remember

1. Weighted graph → **edges have cost/value**.
2. Basic traversal → **DFS/BFS still works**.
3. Weight matters when optimizing **distance/cost/time**.
4. Equal weights → **BFS**.
5. `0/1` weights → **0-1 BFS**.
6. Different non-negative weights → **Dijkstra**.
7. Negative weights → **Bellman-Ford**.
8. **Fewest edges does not mean minimum weighted cost**.