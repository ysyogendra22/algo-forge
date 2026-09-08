# Weighted vs Unweighted Graph

#### 1. Definition — Must Know

1. **Weighted Graph** → Every edge can have a value such as distance, cost, or time.
2. **Unweighted Graph** → Edges have no explicit cost; each edge is usually treated equally.

```text
Weighted:

A --5-- B

Unweighted:

A ----- B
```

#### 2. Weighted Graph — Must Know

Example:

```text
A --4-- B
|       |
2       3
|       |
C --1-- D
```

Weights can represent:

1. Distance between locations.
2. Travel time.
3. Network latency.
4. Price/cost.

A path's cost is typically the **sum of its edge weights**.

```text
A → C → D

Cost = 2 + 1 = 3
```

#### 3. Unweighted Graph — Must Know

```text
A ----- B
|       |
C ----- D
```

1. Every edge is treated as having equal cost.
2. Shortest path usually means the path with the **fewest edges**.
3. **BFS** is the standard shortest-path approach for an unweighted graph.

#### 4. Representation — Must Know

Unweighted adjacency list:

```kotlin
val graph = mutableMapOf<Int, MutableList<Int>>()
```

Example:

```text
1 → [2, 3]
2 → [1]
3 → [1]
```

Weighted adjacency list stores both:

```text
neighbor + weight
```

Kotlin:

```kotlin
data class Edge(
    val to: Int,
    val weight: Int
)

val graph = mutableMapOf<Int, MutableList<Edge>>()
```

Example:

```text
1 → [(2, 5), (3, 2)]
```

means:

```text
1 → 2 costs 5
1 → 3 costs 2
```

#### 5. Choosing Shortest-Path Algorithm — Must Know

```text
Unweighted Graph
      ↓
     BFS

Weighted + Non-negative Weights
      ↓
   Dijkstra

Weighted + Negative Weights
      ↓
 Bellman-Ford
```

This distinction is very important in graph interviews.

#### 6. Important Example — Must Know

```text
A --10-- B

A --1-- C --1-- B
```

Fewest edges:

```text
A → B
Cost = 10
```

Lowest weight:

```text
A → C → B
Cost = 2
```

So in a weighted graph:

**Fewest edges does not necessarily mean shortest/cheapest path.**

#### 7. Complexity & Key Points — Must Know

1. Weighted graph → edges contain an additional **cost/weight**.
2. Unweighted graph → edges are treated equally.
3. BFS shortest path → typically `O(V + E)` for an unweighted graph.
4. Standard Dijkstra with adjacency list + priority queue → `O((V + E) log V)`.
5. Don't use ordinary BFS for general weighted shortest-path problems.
6. Dijkstra requires **non-negative edge weights**.
7. Always inspect the edge weights before choosing a shortest-path algorithm.