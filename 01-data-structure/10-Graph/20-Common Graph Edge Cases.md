# Common Graph Edge Cases

#### 1. Empty Graph — Must Know

```text
V = 0
E = 0
```

1. No vertices or edges.
2. Avoid accessing a start node when the graph is empty.

#### 2. Single Vertex — Must Know

```text
0
```

1. `V = 1`, `E = 0`.
2. BFS/DFS should visit exactly one node.
3. It is also one connected component.

#### 3. Disconnected Graph — Must Know

```text
0 --- 1       2 --- 3
```

1. One BFS/DFS does not visit the whole graph.
2. Loop through every unvisited vertex.

```kotlin
for (node in graph.indices) {
    if (!visited[node]) {
        dfs(node)
    }
}
```

#### 4. Isolated Vertex — Must Know

```text
0 --- 1       2
```

1. Vertex `2` has no edges.
2. It still exists in the graph.
3. It counts as its own connected component.

#### 5. Cycle — Must Know

```text
0 --- 1
|     |
3 --- 2
```

1. Always consider whether cycles are possible.
2. BFS/DFS usually needs `visited`.
3. Without it, traversal may repeatedly revisit nodes.

#### 6. Self-Loop — Must Know

```text
0 ──┐
↑   |
└───┘
```

Edge:

```text
0 → 0
```

1. A self-loop is a cycle.
2. Important for cycle-detection problems.

#### 7. Duplicate / Parallel Edges — Good to Know

```text
A ===== B
```

Multiple edges may connect the same vertices.

Example input:

```text
(0, 1)
(0, 1)
```

1. Don't automatically assume edges are unique.
2. Duplicate edges may affect degree, weight, or algorithm logic depending on the problem.

#### 8. Directed Edge Direction — Must Know

```text
A → B
```

does not imply:

```text
B → A
```

Common mistake:

```kotlin
graph[u].add(v)
graph[v].add(u) // Wrong if graph is directed
```

Always confirm whether the graph is **directed or undirected**.

#### 9. Unreachable Destination — Must Know

```text
0 --- 1       2
```

From `0`, vertex `2` cannot be reached.

For shortest-path problems, use a clear unreachable value such as:

```text
-1
Infinity
```

Do not assume every destination is reachable.

#### 10. Multiple Valid Paths — Must Know

```text
    B
   / \
A     D
   \ /
    C
```

Possible:

```text
A → B → D
A → C → D
```

1. Graphs can have multiple paths between nodes.
2. Traversal order may also have multiple valid answers.
3. Topological Sort can have multiple valid orderings.

#### 11. Negative Edge Weight — Must Know

```text
A --(-5)--> B
```

1. Check edge weights before choosing the shortest-path algorithm.
2. Standard Dijkstra should **not** be used with negative weights.
3. Negative weights → consider **Bellman-Ford** when applicable.

#### 12. Zero-Weight Edge — Good to Know

```text
A --0--> B
```

1. Zero is a valid non-negative weight.
2. Dijkstra can handle zero-weight edges.
3. Don't confuse weight `0` with “no edge” when using a matrix.

#### 13. Deep Graph / Recursion Limit — Good to Know

```text
0 → 1 → 2 → 3 → ... → N
```

Recursive DFS can become very deep.

For very large graphs, iterative DFS may be safer:

```text
Explicit Stack
```

#### 14. Grid Edge Cases — Must Know

For grid-as-graph problems, check:

1. Empty grid.
2. Single cell.
3. All blocked cells.
4. All valid cells.
5. Start = destination.
6. Boundary cells.
7. Correct 4-direction vs 8-direction movement.
8. Multiple disconnected regions.

#### 15. Common Implementation Mistakes — Must Know

1. Forgetting `visited`.
2. Marking BFS nodes visited too late.
3. Forgetting disconnected components.
4. Adding reverse edges to a directed graph.
5. Forgetting reverse edges in an undirected graph.
6. Using BFS for general weighted shortest path.
7. Using Dijkstra with negative weights.
8. Forgetting self-loops or duplicate edges.
9. Assuming every node is reachable.
10. Using the wrong vertex range: `0..n` instead of `0 until n`.

#### 16. Interview Must Remember

Before solving a graph problem, quickly check:

```text
1. Directed or Undirected?
2. Weighted or Unweighted?
3. Cycles possible?
4. Connected or Disconnected?
5. Self-loops / Duplicate edges?
6. Destination reachable?
7. Need visited/state tracking?
```

These checks prevent most common graph implementation mistakes.