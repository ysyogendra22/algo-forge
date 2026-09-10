# Kruskal's Algorithm

#### 1. Definition — Must Know

1. **Kruskal's Algorithm** finds a **Minimum Spanning Tree (MST)** of a weighted, undirected graph.
2. It repeatedly selects the **lowest-weight edge** that does not create a cycle.
3. It uses **Union-Find / DSU** for efficient cycle detection.

```text id="kr01"
Kruskal
   =
Sort Edges by Weight
   +
DSU
```

#### 2. Why It Is Used — Must Know

Use Kruskal when you need to:

```text id="kr02"
Connect all vertices
       +
Minimum total cost
       +
No cycles
```

Example:

```text id="kr03"
Connect cities using minimum road cost.
Connect computers using minimum cable cost.
```

#### 3. Core Idea — Must Know

Consider edges from cheapest to most expensive.

For every edge:

```text id="kr04"
(u, v, weight)
```

Check:

```text id="kr05"
find(u) != find(v)
```

If true:

```text id="kr06"
Different Components
       ↓
Add Edge to MST
       ↓
union(u, v)
```

If:

```text id="kr07"
find(u) == find(v)
```

skip the edge because it would create a cycle.

#### 4. How It Works — Must Know

```text id="kr08"
1. Sort all edges by weight.

2. Initialize DSU.

3. Start MST cost = 0.

4. For every edge from smallest to largest:

   if endpoints are in different components:
       add edge
       union components
       add weight to total cost

   else:
       skip edge

5. Stop after selecting V - 1 edges.
```

#### 5. Example — Must Know

Edges:

```text id="kr09"
A-B → 1
B-C → 2
A-C → 3
C-D → 4
B-D → 5
```

Already sorted.

Process:

```text id="kr10"
A-B → 1   ✓ Add

B-C → 2   ✓ Add

A-C → 3   ✗ Skip
              A and C already connected
              → would create cycle

C-D → 4   ✓ Add
```

For `V = 4`:

```text id="kr11"
Required edges = V - 1 = 3
```

MST:

```text id="kr12"
A-B → 1
B-C → 2
C-D → 4
```

Total:

```text id="kr13"
1 + 2 + 4 = 7
```

#### 6. Graph Representation — Must Know

Kruskal works naturally with an **Edge List**.

```kotlin id="kr14"
data class Edge(
    val u: Int,
    val v: Int,
    val weight: Int
)
```

Example:

```kotlin id="kr15"
val edges = listOf(
    Edge(0, 1, 1),
    Edge(1, 2, 2),
    Edge(0, 2, 3),
    Edge(2, 3, 4)
)
```

#### 7. Kotlin Implementation — Must Know

```kotlin id="kr16"
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

        if (rootA == rootB) {
            return false
        }

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

    var totalCost = 0
    var edgeCount = 0

    for (edge in sortedEdges) {

        if (dsu.union(edge.u, edge.v)) {

            totalCost += edge.weight
            edgeCount++

            if (edgeCount == n - 1) {
                break
            }
        }
    }

    return totalCost
}
```

#### 8. Why DSU Is Used — Must Know

Suppose we want to add:

```text id="kr17"
u ----- v
```

If:

```text id="kr18"
find(u) == find(v)
```

there is already a path connecting them.

Adding another edge creates a cycle.

Therefore:

```text id="kr19"
DSU
 ↓
Fast Connectivity Check
 ↓
Cycle Detection
```

#### 9. Why Stop at `V - 1` Edges? — Must Know

A tree with `V` vertices always contains:

```text id="kr20"
V - 1 edges
```

Once Kruskal selects `V - 1` valid edges:

```text id="kr21"
All vertices connected
+
No cycles
=
Spanning Tree
```

No more edges are required.

#### 10. Time & Space Complexity — Must Know

Sorting:

```text id="kr22"
O(E log E)
```

DSU operations:

```text id="kr23"
O(E × α(V))
```

Overall:

```text id="kr24"
Time → O(E log E)
```

because sorting dominates.

Space:

```text id="kr25"
DSU        → O(V)
Edge List  → O(E)

Total → O(V + E)
```

#### 11. Kruskal vs Prim — Must Know

```text id="kr26"
Kruskal                    Prim

Chooses cheapest edge      Grows from a vertex

Edge List                  Adjacency List

Sort edges                 Min-Heap

DSU                        Visited

Builds components          Builds one tree outward

O(E log E)                 O(E log V)
```

Simple memory:

```text id="kr27"
Kruskal → Edges + DSU

Prim → Nodes + Min-Heap
```

#### 12. Disconnected Graph — Good to Know

If the graph is disconnected, Kruskal cannot produce one MST.

Instead it produces a:

```text id="kr28"
Minimum Spanning Forest
```

To verify an MST exists:

```kotlin id="kr29"
if (edgeCount != n - 1) {
    // Graph is disconnected
}
```

#### 13. Common Interview Patterns — Must Know

1. Minimum cost to connect cities.
2. Minimum cost to connect points.
3. Network/cable connection cost.
4. Add cheapest edges without creating cycles.
5. Problems that naturally provide an **edge list**.

#### 14. Common Mistakes — Must Know

1. Forgetting to sort edges by weight.
2. Adding an edge without checking for a cycle.
3. Using plain `visited` instead of DSU for Kruskal.
4. Forgetting `union()` after selecting an edge.
5. Continuing unnecessarily after `V - 1` edges.
6. Assuming a disconnected graph has an MST.
7. Confusing Kruskal with shortest-path algorithms.

#### 15. Interview Must Remember

1. Kruskal finds an **MST**.
2. Works on **weighted, undirected graphs**.
3. Sort edges from **smallest → largest weight**.
4. Add an edge only if it does **not create a cycle**.
5. Use **DSU** for cycle detection.
6. Stop after **`V - 1` edges**.
7. Complexity → **`O(E log E)`**.
8. **Kruskal = Sort Edges + DSU**.