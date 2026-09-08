# Graph Fundamentals

#### 1. Definition — Must Know

1. A **Graph** is a non-linear data structure representing relationships between objects.
2. It consists of:
   - **Vertices (Nodes)** → Objects.
   - **Edges** → Connections between objects.
3. Graphs are more general than trees and can contain **cycles, multiple paths, and disconnected components**.

#### 2. Why It Is Used — Must Know

1. Used when data represents **connections or relationships**.
2. Common examples:
   - Social networks → users + connections.
   - Maps → locations + roads.
   - Computer networks → devices + connections.
   - Dependencies → tasks/services + dependencies.
   - Recommendation systems → users/items + relationships.

#### 3. How It Works — Must Know

Example:

```text
A ----- B
|       |
|       |
C ----- D
```

```text
Vertices → A, B, C, D

Edges →
A-B
A-C
B-D
C-D
```

Unlike a tree, multiple paths can exist:

```text
A → B → D

A → C → D
```

#### 4. Core Terminology — Must Know

1. **Vertex / Node** — Individual element in a graph.
2. **Edge** — Connection between two vertices.
3. **Adjacent / Neighbor** — Directly connected vertices.
4. **Path** — Sequence of connected vertices.
5. **Cycle** — Path that eventually returns to a previously visited node.
6. **Degree** — Number of edges connected to a vertex.
7. **Connected Graph** — Every vertex is reachable from every other vertex.
8. **Connected Component** — Connected section of a potentially disconnected graph.

#### 5. Graph Types — Must Know

**Undirected Graph**

```text
A ----- B
```

Connection works both ways:

```text
A ↔ B
```

Example → Facebook-style friendship.

**Directed Graph**

```text
A ----> B
```

Direction matters:

```text
A → B ≠ B → A
```

Example → dependencies or social-media following.

**Weighted Graph**

```text
A --5-- B
```

Edge contains a cost/weight.

Examples:

```text
Distance
Time
Price
Network cost
```

**Unweighted Graph**

```text
A ----- B
```

Edges have no meaningful cost or are treated equally.

#### 6. Cyclic vs Acyclic — Must Know

**Cyclic**

```text
A → B
↑   ↓
└── C
```

Contains a cycle.

**Acyclic**

```text
A → B → C
```

Contains no cycle.

A **DAG** is a:

```text
Directed Acyclic Graph
```

DAGs are important for dependency and scheduling problems.

#### 7. Tree vs Graph — Must Know

```text
Tree                         Graph

Connected                    May be disconnected
No cycles                    May contain cycles
N nodes → N-1 edges          No such restriction
Unique path between nodes    Multiple paths may exist
Hierarchical                 General relationships
```

A tree is a **special type of graph**.

#### 8. Basic Graph Representation — Must Know

The most common interview representation is an **Adjacency List**.

Graph:

```text
A ----- B
|
C
```

Representation:

```text
A → [B, C]
B → [A]
C → [A]
```

Kotlin:

```kotlin
val graph = mutableMapOf<Int, MutableList<Int>>()

fun addEdge(u: Int, v: Int) {
    graph.getOrPut(u) { mutableListOf() }.add(v)
    graph.getOrPut(v) { mutableListOf() }.add(u)
}
```

For a **directed graph**, add only:

```kotlin
graph.getOrPut(u) { mutableListOf() }.add(v)
```

#### 9. Adjacency List vs Matrix — Must Know

**Adjacency List**

```text
A → B, C
B → A
C → A
```

Space:

```text
O(V + E)
```

Usually preferred for interview problems.

**Adjacency Matrix**

```text
    A B C
A   0 1 1
B   1 0 0
C   1 0 0
```

Space:

```text
O(V²)
```

Useful when quick edge-existence lookup matters or the graph is dense.

#### 10. Graph Traversal — Must Know

Two fundamental algorithms:

```text
DFS → Depth-First Search
BFS → Breadth-First Search
```

Typical traversal complexity with adjacency lists:

```text
Time  → O(V + E)
Space → O(V)
```

Study BFS and DFS separately in depth.

#### 11. Key Points — Must Know

1. Graph = **Vertices + Edges**.
2. First identify: **directed or undirected**.
3. Check whether edges are **weighted or unweighted**.
4. Graphs may contain **cycles**, so traversal usually needs a `visited` structure.
5. Graphs may be **disconnected**, so one BFS/DFS may not visit every vertex.
6. **Adjacency List** is the most common graph representation for interviews.
7. Graph traversal complexity is typically `O(V + E)`.
8. **BFS and DFS** are the foundation for most graph algorithms.