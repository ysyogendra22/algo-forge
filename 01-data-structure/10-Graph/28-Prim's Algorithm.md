# Prim's Algorithm

#### 1. Definition — Must Know

1. **Prim's Algorithm** finds a **Minimum Spanning Tree (MST)** of a weighted, undirected graph.
2. It starts from any vertex and grows **one connected tree**.
3. At every step, choose the **minimum-weight edge** connecting the current tree to an unvisited vertex.
4. Usually implemented using a **Min-Heap / Priority Queue**.

```text id="pr01"
Prim
 =
Adjacency List
+
Min-Heap
+
Visited
```

#### 2. Why It Is Used — Must Know

Use Prim when you need to:

```text id="pr02"
Connect all vertices
       +
Minimum total cost
       +
No cycles
```

Example:

```text id="pr03"
Minimum cost to connect cities
Minimum cable/network cost
Minimum road connection cost
```

#### 3. Core Idea — Must Know

Start from any vertex:

```text id="pr04"
A
```

Add the cheapest edge connecting the current MST to an unvisited node:

```text id="pr05"
A --2-- B
```

Then continue:

```text id="pr06"
A --2-- B --3-- C
```

The tree grows one vertex at a time.

#### 4. How It Works — Must Know

```text id="pr07"
1. Start from any vertex.

2. Add it to Min-Heap with cost 0.

3. Remove the minimum-cost entry.

4. If node already visited:
      skip it.

5. Otherwise:
      mark visited.
      add edge cost to MST.

6. Add all unvisited neighbors to Min-Heap.

7. Continue until all vertices are visited.
```

#### 5. Example — Must Know

Graph:

```text id="pr08"
A ----1---- B
|           |
4           2
|           |
C ----3---- D
```

Start from `A`.

Initial:

```text id="pr09"
Heap → (A, 0)
```

Visit `A`:

```text id="pr10"
Candidates:

A-B → 1
A-C → 4
```

Choose:

```text id="pr11"
A-B → 1
```

Now candidates include:

```text id="pr12"
B-D → 2
A-C → 4
```

Choose:

```text id="pr13"
B-D → 2
```

Then:

```text id="pr14"
D-C → 3
```

MST cost:

```text id="pr15"
1 + 2 + 3 = 6
```

#### 6. Graph Representation — Must Know

Prim naturally uses a **weighted adjacency list**.

```kotlin id="pr16"
data class Edge(
    val to: Int,
    val weight: Int
)

val graph = Array(n) {
    mutableListOf<Edge>()
}
```

For an undirected graph:

```kotlin id="pr17"
graph[u].add(Edge(v, weight))
graph[v].add(Edge(u, weight))
```

#### 7. Kotlin Implementation — Must Know

```kotlin id="pr18"
import java.util.PriorityQueue

data class Edge(
    val to: Int,
    val weight: Int
)

data class State(
    val node: Int,
    val weight: Int
)

fun prim(
    n: Int,
    graph: Array<MutableList<Edge>>
): Int {

    val visited = BooleanArray(n)

    val pq = PriorityQueue<State>(
        compareBy { it.weight }
    )

    pq.offer(State(0, 0))

    var totalCost = 0
    var visitedCount = 0

    while (pq.isNotEmpty()) {

        val current = pq.poll()

        if (visited[current.node]) {
            continue
        }

        visited[current.node] = true
        visitedCount++

        totalCost += current.weight

        for (edge in graph[current.node]) {

            if (!visited[edge.to]) {
                pq.offer(
                    State(edge.to, edge.weight)
                )
            }
        }
    }

    return totalCost
}
```

#### 8. Why Start with Weight `0`? — Must Know

Initial source:

```text id="pr19"
(source, 0)
```

The source does not require an edge to enter the MST.

Therefore:

```text id="pr20"
Initial contribution = 0
```

After that, each selected node contributes the edge cost used to connect it.

#### 9. Why `visited` Is Important — Must Know

The Priority Queue may contain multiple edges leading to the same node.

Example:

```text id="pr21"
A --5-- C
B --2-- C
```

Heap may contain:

```text id="pr22"
(C, 5)
(C, 2)
```

Once `C` is selected using cost `2`, later:

```text id="pr23"
(C, 5)
```

must be skipped.

Hence:

```kotlin id="pr24"
if (visited[current.node]) {
    continue
}
```

#### 10. Cycle Prevention — Must Know

Prim does not normally need DSU.

It prevents cycles using:

```text id="pr25"
visited
```

Only edges leading to unvisited vertices are accepted.

Compare:

```text id="pr26"
Kruskal → DSU prevents cycles

Prim    → visited prevents cycles
```

#### 11. Time & Space Complexity — Must Know

Using:

```text id="pr27"
Adjacency List + Min-Heap
```

Time:

```text id="pr28"
O(E log V)
```

Space:

```text id="pr29"
Graph    → O(V + E)
Visited  → O(V)
Heap     → up to O(E)

Total → O(V + E)
```

#### 12. Prim vs Dijkstra — Must Know

They look similar because both use a Min-Heap, but their goals are different.

```text id="pr30"
Prim                       Dijkstra

Find MST                   Find shortest paths

Minimum edge weight        Minimum total path distance

Connect all vertices       Distance from source

Heap stores edge cost      Heap stores path distance

No distance array needed   Distance array needed
```

Most important difference:

```text id="pr31"
Prim:
priority = edge.weight

Dijkstra:
priority = distance[node] + edge.weight
```

#### 13. Prim vs Kruskal — Must Know

```text id="pr32"
Prim                       Kruskal

Starts from a vertex       Starts with sorted edges

Grows one tree             Merges components

Adjacency List             Edge List

Min-Heap                   Sorting

Visited                    DSU

O(E log V)                 O(E log E)
```

Easy memory:

```text id="pr33"
Prim
→ Nodes + Min-Heap

Kruskal
→ Edges + DSU
```

#### 14. Disconnected Graph — Good to Know

A single MST requires the graph to be connected.

After Prim:

```kotlin id="pr34"
if (visitedCount != n) {
    // Graph is disconnected
    // No single MST exists
}
```

For a disconnected graph, you can build a:

```text id="pr35"
Minimum Spanning Forest
```

#### 15. Common Interview Patterns — Must Know

1. Minimum cost to connect all nodes.
2. Minimum road/network/cable cost.
3. Weighted undirected graph requiring an MST.
4. Graph already given as an adjacency list.
5. Grow the cheapest connected network from a node.

#### 16. Common Mistakes — Must Know

1. Confusing Prim with Dijkstra.
2. Using cumulative source distance instead of edge weight.
3. Forgetting `visited`.
4. Adding the cost of an already visited node.
5. Forgetting the graph is undirected.
6. Assuming a disconnected graph has one MST.
7. Using DSU unnecessarily with standard Prim.

#### 17. Interview Must Remember

1. Prim finds a **Minimum Spanning Tree**.
2. Works on a **weighted, undirected graph**.
3. Starts from any vertex and **grows one tree**.
4. Always choose the cheapest edge to an **unvisited vertex**.
5. Uses **Adjacency List + Min-Heap + Visited**.
6. Complexity → **`O(E log V)`** with a heap.
7. **Prim uses edge weight; Dijkstra uses total path distance.**
8. **Prim = Min-Heap + Visited; Kruskal = Sorted Edges + DSU.**