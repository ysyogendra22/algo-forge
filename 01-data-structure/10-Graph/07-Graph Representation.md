# Graph Representation

#### 1. Definition — Must Know

1. Graph representation means **how vertices and edges are stored in memory**.
2. Two main representations:
   - **Adjacency List** — Must Know.
   - **Adjacency Matrix** — Must Know.
3. **Edge List** — Good to Know.

#### 2. Adjacency List — Must Know

Stores each vertex with its neighbors.

Graph:

```text
0 ----- 1
|       |
2 ----- 3
```

Representation:

```text
0 → [1, 2]
1 → [0, 3]
2 → [0, 3]
3 → [1, 2]
```

Kotlin:

```kotlin
val graph = Array(4) { mutableListOf<Int>() }

fun addEdge(u: Int, v: Int) {
    graph[u].add(v)
    graph[v].add(u)
}
```

For a directed graph:

```kotlin
fun addEdge(u: Int, v: Int) {
    graph[u].add(v)
}
```

#### 3. Adjacency List Complexity — Must Know

```text
Space                  → O(V + E)
Iterate neighbors      → O(degree(V))
Check specific edge    → O(degree(V))
```

1. Best choice for **sparse graphs**.
2. Most common representation in FAANG graph problems.
3. Works naturally with **BFS and DFS**.

#### 4. Weighted Adjacency List — Must Know

Store both neighbor and weight.

```text
0 --5-- 1
|
2
|
2
```

Representation:

```text
0 → [(1,5), (2,2)]
```

Kotlin:

```kotlin
data class Edge(
    val to: Int,
    val weight: Int
)

val graph = Array(4) { mutableListOf<Edge>() }

fun addEdge(u: Int, v: Int, weight: Int) {
    graph[u].add(Edge(v, weight))
    graph[v].add(Edge(u, weight))
}
```

Common with:

```text
Dijkstra
Prim's Algorithm
Weighted graph traversal
```

#### 5. Adjacency Matrix — Must Know

Uses a `V × V` matrix.

Graph:

```text
0 ----- 1
|
2
```

Representation:

```text
    0  1  2

0   0  1  1
1   1  0  0
2   1  0  0
```

Kotlin:

```kotlin
val graph = Array(3) { IntArray(3) }

fun addEdge(u: Int, v: Int) {
    graph[u][v] = 1
    graph[v][u] = 1
}
```

For directed:

```kotlin
graph[u][v] = 1
```

#### 6. Adjacency Matrix Complexity — Must Know

```text
Space                  → O(V²)
Check specific edge    → O(1)
Iterate neighbors      → O(V)
```

Best when:

1. Graph is **dense**.
2. Fast edge lookup is important.
3. Number of vertices is relatively small.

#### 7. Edge List — Good to Know

Simply store all edges.

```text
0 ----- 1
|
2
```

Representation:

```text
(0,1)
(0,2)
```

Kotlin:

```kotlin
data class Edge(
    val from: Int,
    val to: Int,
    val weight: Int
)

val edges = mutableListOf<Edge>()
```

Useful for algorithms that primarily process edges.

Examples:

```text
Kruskal's Algorithm
Bellman-Ford
```

#### 8. Comparison — Must Know

```text
                    Adjacency List     Adjacency Matrix

Space               O(V + E)           O(V²)
Edge lookup          O(degree)          O(1)
Neighbor traversal   O(degree)          O(V)
Sparse graph         Best               Wasteful
Dense graph          Good               Good
BFS / DFS            Preferred          Possible
```

#### 9. Common Interview Choice — Must Know

For most problems, start with:

```kotlin
val graph = Array(n) { mutableListOf<Int>() }
```

Then build:

```kotlin
for ((u, v) in edges) {
    graph[u].add(v)
    graph[v].add(u)
}
```

For directed graphs, remove the reverse edge.

#### 10. Key Points — Must Know

1. **Adjacency List** → default choice for most interview problems.
2. Adjacency List space → `O(V + E)`.
3. Adjacency Matrix space → `O(V²)`.
4. Matrix gives `O(1)` edge lookup.
5. Undirected graph → normally store edge in **both directions**.
6. Directed graph → store only the given direction.
7. Weighted graph → store **neighbor + weight**.
8. **Edge List** is useful when the algorithm works directly with edges.