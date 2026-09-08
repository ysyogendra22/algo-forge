# Directed vs Undirected Graph

#### 1. Definition — Must Know

1. **Directed Graph** → Edges have a direction.
2. **Undirected Graph** → Edges have no direction and work both ways.

```text id="du001"
Directed:

A → B

Undirected:

A — B
```

#### 2. Directed Graph — Must Know

```text id="du002"
A → B → C
```

1. `A → B` means A can reach B directly.
2. It does **not** automatically mean `B → A`.
3. Relationships are one-way unless the reverse edge also exists.

Examples:

1. Social media following.
2. Task dependencies.
3. Course prerequisites.
4. Web page links.

#### 3. Undirected Graph — Must Know

```text id="du003"
A — B — C
```

An edge:

```text id="du004"
A — B
```

means:

```text id="du005"
A → B
B → A
```

Examples:

1. Friendship relationships.
2. Two-way roads.
3. Physical network connections.

#### 4. Adjacency List Representation — Must Know

For:

```text id="du006"
A → B
```

Directed:

```text id="du007"
A → [B]
B → []
```

Only one direction is stored.

For:

```text id="du008"
A — B
```

Undirected:

```text id="du009"
A → [B]
B → [A]
```

Store the edge in **both directions**.

#### 5. Kotlin Implementation — Must Know

Directed:

```kotlin id="du010"
fun addDirectedEdge(
    graph: MutableMap<Int, MutableList<Int>>,
    from: Int,
    to: Int
) {
    graph.getOrPut(from) { mutableListOf() }.add(to)
}
```

Undirected:

```kotlin id="du011"
fun addUndirectedEdge(
    graph: MutableMap<Int, MutableList<Int>>,
    u: Int,
    v: Int
) {
    graph.getOrPut(u) { mutableListOf() }.add(v)
    graph.getOrPut(v) { mutableListOf() }.add(u)
}
```

#### 6. Degree — Must Know

Undirected:

```text id="du012"
Degree = Number of connected edges
```

Directed:

```text id="du013"
In-degree  → Incoming edges
Out-degree → Outgoing edges
```

Example:

```text id="du014"
A → B ← C
    |
    ↓
    D
```

For `B`:

```text id="du015"
In-degree  = 2
Out-degree = 1
```

#### 7. Traversal Difference — Must Know

Consider:

```text id="du016"
A → B
```

Directed:

```text id="du017"
From A → B reachable
From B → A not necessarily reachable
```

Undirected:

```text id="du018"
A — B

From A → B reachable
From B → A reachable
```

BFS and DFS algorithms are largely the same; the **stored edges determine where traversal can move**.

#### 8. Cycle Detection Difference — Must Know

Cycle detection logic differs.

**Undirected Graph**

1. During DFS, track the **parent**.
2. A visited neighbor that is not the parent indicates a cycle.

**Directed Graph**

1. A simple `visited` set alone is not enough.
2. Common DFS approach tracks nodes in the **current recursion path/state**.
3. Encountering a node already in the current path indicates a cycle.

Study the implementations separately under **Cycle Detection**.

#### 9. Key Differences — Must Know

```text id="du019"
                     Directed            Undirected

Edge                 A → B               A — B
Direction            One-way             Both ways
Adjacency List       Store once          Store both ways
Degree                In / Out degree     Degree
Reachability          Direction matters   Bidirectional
Cycle Detection       DFS state/path       DFS + parent
```

#### 10. Key Points — Must Know

1. First identify whether the graph is **directed or undirected**.
2. Directed → `A → B` does not imply `B → A`.
3. Undirected → store every edge in **both adjacency lists**.
4. Directed graphs have **in-degree and out-degree**.
5. BFS/DFS fundamentals remain similar, but **reachability changes with direction**.
6. Cycle-detection logic is different for directed and undirected graphs.