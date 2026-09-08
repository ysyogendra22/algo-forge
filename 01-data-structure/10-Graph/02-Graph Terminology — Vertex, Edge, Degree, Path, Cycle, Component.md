# Graph Terminology

#### 1. Vertex / Node — Must Know

1. A **Vertex (Node)** represents an individual object in a graph.
2. Usually represented as `V`.

```text
A ----- B
     	
A and B → Vertices
```

Examples:

1. Social network → User.
2. Map → City.
3. Computer network → Device.

#### 2. Edge — Must Know

1. An **Edge** represents a connection between two vertices.
2. Usually represented as `E`.

```text
A ----- B

A-B → Edge
```

Types:

1. **Undirected Edge** → `A ↔ B`.
2. **Directed Edge** → `A → B`.
3. **Weighted Edge** → Edge contains cost/distance/time.

#### 3. Degree — Must Know

1. **Degree** → Number of edges connected to a vertex.

```text
    B
    |
C---A---D
```

```text
Degree(A) = 3
Degree(B) = 1
```

For a **directed graph**:

1. **In-degree** → Number of incoming edges.
2. **Out-degree** → Number of outgoing edges.

```text
A → B → C
    ↑
    D
```

For `B`:

```text
In-degree  = 2
Out-degree = 1
```

In-degree is especially important for **Topological Sort / Kahn's Algorithm**.

#### 4. Path — Must Know

1. A **Path** is a sequence of vertices connected by edges.

```text
A → B → C → D
```

Path from `A` to `D`:

```text
A → B → C → D
```

2. **Path length** is commonly the number of edges in the path.
3. In weighted graphs, path cost is usually the sum of edge weights.

#### 5. Cycle — Must Know

1. A **Cycle** exists when a path returns to a previously visited vertex.

```text
A → B
↑   ↓
C ←─
```

```text
A → B → C → A
```

2. Graphs can be **cyclic or acyclic**.
3. Cycle detection is a common interview pattern.
4. Directed and undirected graphs require slightly different cycle-detection logic.

#### 6. Connected Component — Must Know

1. A **Connected Component** is a group of vertices connected to each other.
2. A graph can contain multiple separate components.

```text
A --- B       D --- E
      |       
      C          

Component 1 → A, B, C
Component 2 → D, E
```

Number of components:

```text
2
```

3. Components are commonly found using **DFS or BFS**.
4. For directed graphs, connectivity has more specific forms such as **strongly connected components**; study those only when needed.

#### 7. Related Terms — Good to Know

1. **Neighbor / Adjacent** — Vertices directly connected by an edge.
2. **Self-loop** — Edge from a vertex to itself.
3. **Connected Graph** — All vertices belong to one connected component.
4. **Disconnected Graph** — Contains multiple components.
5. **DAG** — Directed graph containing no cycles.

#### 8. Key Points — Must Know

1. `V` → Number of **vertices**.
2. `E` → Number of **edges**.
3. **Degree** → Number of connected edges.
4. Directed graph → know **in-degree and out-degree**.
5. **Path** → Sequence of connected vertices.
6. **Cycle** → Path that loops back to an already visited vertex.
7. **Component** → Connected group of vertices.
8. These concepts appear constantly in **BFS, DFS, cycle detection, shortest path, and topological sort**.