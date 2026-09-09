# Graph Time & Space Complexity

#### 1. Core Terms — Must Know

1. `V` → Number of **Vertices / Nodes**.
2. `E` → Number of **Edges**.
3. Most graph complexity is expressed using `V` and `E`.

```text
V = Vertices
E = Edges
```

#### 2. Graph Representation — Must Know

**Adjacency List**

```text
Space → O(V + E)
```

Why:

1. Store `V` vertices.
2. Store their edges.
3. In an undirected graph, each edge is stored twice, but complexity remains `O(E)`.

**Adjacency Matrix**

```text
Space → O(V²)
```

Because every possible pair of vertices gets a matrix entry.

#### 3. BFS Complexity — Must Know

```text
Time  → O(V + E)
Space → O(V)
```

Why:

1. Every vertex is visited once.
2. Every edge is examined.
3. Queue + visited can hold up to `V` nodes.

If including graph storage:

```text
Total Space → O(V + E)
```

#### 4. DFS Complexity — Must Know

```text
Time  → O(V + E)
Space → O(V)
```

Why:

1. Every vertex is visited once.
2. Every edge is examined.
3. `visited` + recursion/stack can require `O(V)`.

If including graph storage:

```text
Total Space → O(V + E)
```

#### 5. Connected Components — Must Know

Using DFS/BFS:

```text
Time  → O(V + E)
Space → O(V)
```

Even though DFS/BFS may start multiple times, each vertex and edge is still processed only a constant number of times overall.

#### 6. Cycle Detection — Must Know

Undirected:

```text
DFS/BFS + Parent

Time  → O(V + E)
Space → O(V)
```

Directed:

```text
DFS + State/Current Path

Time  → O(V + E)
Space → O(V)
```

#### 7. Topological Sort — Must Know

Kahn's Algorithm:

```text
Time  → O(V + E)
Space → O(V)
```

DFS Topological Sort:

```text
Time  → O(V + E)
Space → O(V)
```

Extra space comes from:

```text
Queue / DFS Stack
In-degree / Visited
Result
```

#### 8. Shortest Path — Must Know

**Unweighted Graph — BFS**

```text
Time  → O(V + E)
Space → O(V)
```

**Dijkstra — Adjacency List + Min-Heap**

```text
Time  → O((V + E) log V)
Space → O(V + E)
```

Graph storage contributes `O(V + E)`.

Extra algorithmic structures include the distance array and priority queue.

#### 9. Grid as Graph — Must Know

For:

```text
Rows = R
Columns = C
```

Number of vertices:

```text
V = R × C
```

Each cell normally has at most 4 or 8 neighbors.

Therefore DFS/BFS:

```text
Time  → O(R × C)
Space → O(R × C)
```

Common for:

1. Number of Islands.
2. Flood Fill.
3. Rotting Oranges.
4. Grid shortest path.

#### 10. Sparse vs Dense Graph — Good to Know

**Sparse Graph**

Few edges:

```text
E ≈ V
```

Adjacency List is usually preferred.

**Dense Graph**

Many edges:

```text
E ≈ V²
```

Adjacency Matrix may become reasonable when fast edge lookup is important.

#### 11. Important Complexity Table — Must Know

| Operation / Algorithm | Time | Extra Space |
|---|---:|---:|
| BFS | `O(V + E)` | `O(V)` |
| DFS | `O(V + E)` | `O(V)` |
| Connected Components | `O(V + E)` | `O(V)` |
| Cycle Detection | `O(V + E)` | `O(V)` |
| Topological Sort | `O(V + E)` | `O(V)` |
| Unweighted Shortest Path | `O(V + E)` | `O(V)` |
| Dijkstra | `O((V+E) log V)` | up to `O(V+E)` |
| Grid DFS/BFS | `O(R × C)` | `O(R × C)` |

#### 12. Common Interview Mistakes — Must Know

1. Saying graph traversal is simply `O(V)` and forgetting edges.
2. Forgetting adjacency-list storage → `O(V + E)`.
3. Saying adjacency matrix uses `O(V + E)` instead of `O(V²)`.
4. Forgetting recursive DFS uses stack space.
5. Assuming running DFS multiple times for components means `O(V × (V+E))`; visited prevents that.
6. Forgetting grid complexity is usually based on total cells: `R × C`.

#### 13. Interview Must Remember

1. Graph traversal → usually **`O(V + E)`**.
2. Adjacency List → **`O(V + E)` space**.
3. Adjacency Matrix → **`O(V²)` space**.
4. BFS/DFS extra space → **`O(V)`**.
5. Grid traversal → **`O(R × C)`**.
6. Dijkstra with Min-Heap → roughly **`O((V + E) log V)`**.
7. When stating space complexity, clarify whether you mean **extra algorithm space** or **graph storage + algorithm space**.