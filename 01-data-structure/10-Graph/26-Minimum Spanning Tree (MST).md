# Minimum Spanning Tree (MST)

#### 1. Definition — Must Know

1. A **Minimum Spanning Tree (MST)** connects all vertices of a **weighted, undirected graph**.
2. It uses the **minimum possible total edge weight**.
3. It contains **no cycles**.
4. For `V` vertices, an MST always contains:

```text id="mst01"
V - 1 edges
```

#### 2. What Is a Spanning Tree? — Must Know

A spanning tree:

1. Includes **all vertices**.
2. Keeps them connected.
3. Contains no cycles.
4. Has exactly `V - 1` edges.

Example:

```text id="mst02"
Original:

A ----- B
| \     |
|   \   |
C ----- D


Possible Spanning Tree:

A ----- B
|
C ----- D
```

An MST is the spanning tree with the **lowest total cost**.

#### 3. Example — Must Know

Weighted graph:

```text id="mst03"
A ----1---- B
|           |
4           2
|           |
C ----3---- D
```

One MST:

```text id="mst04"
A --1-- B
        |
        2
        |
C --3-- D
```

Total:

```text id="mst05"
1 + 2 + 3 = 6
```

We avoid the edge with weight `4`.

#### 4. Core Properties — Must Know

An MST:

```text id="mst06"
Connected
+
All Vertices
+
No Cycles
+
V - 1 Edges
+
Minimum Total Weight
```

Important:

1. MST is mainly defined for **connected, weighted, undirected graphs**.
2. A graph can have **multiple valid MSTs** with the same minimum cost.
3. If all relevant edge weights are distinct, the MST is unique.
4. Removing any MST edge disconnects the tree.

#### 5. Main MST Algorithms — Must Know

Two algorithms:

```text id="mst07"
Kruskal's Algorithm
Prim's Algorithm
```

Both find an MST but use different approaches.

#### 6. Kruskal's Algorithm — Must Know

Core idea:

```text id="mst08"
Choose globally cheapest edges
while avoiding cycles.
```

Steps:

```text id="mst09"
1. Sort all edges by weight.

2. Start with no edges.

3. Pick the smallest edge.

4. If it does NOT create a cycle:
      include it.

5. Otherwise:
      skip it.

6. Stop after V - 1 edges.
```

Cycle detection is efficiently handled using:

```text id="mst10"
Union-Find / DSU
```

Think:

```text id="mst11"
Kruskal
   =
Sorted Edges
   +
DSU
```

#### 7. Kruskal Example

Edges:

```text id="mst12"
A-B → 1
B-D → 2
C-D → 3
A-C → 4
```

Already sorted.

Pick:

```text id="mst13"
A-B → 1   ✓
B-D → 2   ✓
C-D → 3   ✓
```

Now:

```text id="mst14"
Edges = V - 1
```

Done.

Total:

```text id="mst15"
6
```

#### 8. Kotlin — Kruskal — Must Know

```kotlin id="mst16"
data class Edge(
    val u: Int,
    val v: Int,
    val weight: Int
)

class DSU(n: Int) {

    private val parent = IntArray(n) { it }
    private val size = IntArray(n) { 1 }

    fun find(x: Int): Int {

        if (parent[x] != x) {
            parent[x] = find(parent[x])
        }

        return parent[x]
    }

    fun union(a: Int, b: Int): Boolean {

        var rootA = find(a)
        var rootB = find(b)

        if (rootA == rootB) return false

        if (size[rootA] < size[rootB]) {
            val temp = rootA
            rootA = rootB
            rootB = temp
        }

        parent[rootB] = rootA
        size[rootA] += size[rootB]

        return true
    }
}

fun kruskal(
    n: Int,
    edges: List<Edge>
): Int {

    val sortedEdges = edges.sortedBy { it.weight }

    val dsu = DSU(n)

    var totalWeight = 0
    var edgeCount = 0

    for (edge in sortedEdges) {

        if (dsu.union(edge.u, edge.v)) {

            totalWeight += edge.weight
            edgeCount++

            if (edgeCount == n - 1) {
                break
            }
        }
    }

    return totalWeight
}
```

#### 9. Prim's Algorithm — Must Know

Core idea:

```text id="mst17"
Start from one vertex
        ↓
Grow one connected tree
        ↓
Always choose cheapest edge
connecting tree to an unvisited vertex
```

Uses:

```text id="mst18"
Adjacency List
+
Min-Heap / Priority Queue
+
Visited
```

Think:

```text id="mst19"
Prim
 =
Graph Traversal
 +
Min-Heap
```

#### 10. Prim vs Kruskal — Must Know

```text id="mst20"
Kruskal                     Prim

Works edge-by-edge           Grows from a vertex

Sort all edges               Uses Min-Heap

Uses DSU                     Uses Visited

Avoid cycles using DSU       Avoid revisiting vertices

Great with edge list         Great with adjacency list
```

For interviews, know both.

#### 11. Complexity — Must Know

**Kruskal**

Sorting edges dominates:

```text id="mst21"
Time  → O(E log E)
Space → O(V + E)
```

DSU operations are nearly constant amortized.

**Prim with Min-Heap**

```text id="mst22"
Time  → O(E log V)
Space → O(V + E)
```

#### 12. MST vs Shortest Path — Must Know

Do not confuse these.

```text id="mst23"
MST                         Shortest Path

Connect all vertices        Find shortest route

Minimize total tree cost    Minimize path distance

Kruskal / Prim              BFS / Dijkstra

No source required          Usually starts from source
```

Example:

```text id="mst24"
"Connect all cities with minimum cable cost"
                 ↓
                MST


"Find cheapest route from A to B"
                 ↓
          Shortest Path
```

#### 13. Disconnected Graph — Good to Know

If the graph is disconnected:

```text id="mst25"
No single spanning tree exists.
```

Instead, you can get a:

```text id="mst26"
Minimum Spanning Forest
```

One minimum spanning tree for each connected component.

#### 14. Common Interview Patterns — Must Know

1. **Connect all cities with minimum cost**
   ```text
   MST
   ```

2. **Connect computers/networks with minimum cable**
   ```text
   MST
   ```

3. **Minimum cost to connect points**
   ```text
   MST
   ```

4. **Choose cheapest connections without cycles**
   ```text
   Kruskal + DSU
   ```

5. **Grow cheapest network from a starting node**
   ```text
   Prim
   ```

#### 15. Common Mistakes — Must Know

1. Confusing MST with shortest path.
2. Forgetting MST needs all vertices connected.
3. Forgetting an MST has exactly `V - 1` edges.
4. Allowing cycles.
5. Using Kruskal without sorting edges.
6. Forgetting DSU cycle detection in Kruskal.
7. Assuming MST is always unique.
8. Assuming a disconnected graph has one MST.

#### 16. Interview Must Remember

1. MST → connect **all vertices with minimum total cost**.
2. MST contains **no cycles**.
3. `V` vertices → exactly **`V - 1` edges**.
4. **Kruskal = Sorted Edges + DSU**.
5. **Prim = Adjacency List + Min-Heap + Visited**.
6. Kruskal → `O(E log E)`.
7. Prim → `O(E log V)`.
8. **MST minimizes total network cost; Dijkstra minimizes path distance.**