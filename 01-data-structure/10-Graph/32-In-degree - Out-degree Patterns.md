# In-degree / Out-degree Patterns

#### 1. Definition — Must Know

For a **directed graph**:

```text
A → B
```

1. **Out-degree of A** → number of edges leaving `A`.
2. **In-degree of B** → number of edges entering `B`.

```text
In-degree  = Incoming edges
Out-degree = Outgoing edges
```

#### 2. Example — Must Know

```text
A → B
A → C
B → C
```

Degrees:

```text
Node    In-degree    Out-degree

A          0             2
B          1             1
C          2             0
```

#### 3. How to Calculate — Must Know

For every directed edge:

```text
u → v
```

Update:

```kotlin
outdegree[u]++
indegree[v]++
```

Implementation:

```kotlin
val indegree = IntArray(n)
val outdegree = IntArray(n)

for ((u, v) in edges) {
    outdegree[u]++
    indegree[v]++
}
```

#### 4. Source and Sink — Must Know

**Source**

```text
In-degree = 0
```

No incoming dependency.

**Sink**

```text
Out-degree = 0
```

No outgoing edge.

Example:

```text
A → B → C
```

```text
A → Source
C → Sink
```

#### 5. Topological Sort Pattern — Must Know

In dependency graphs:

```text
inDegree[node] = number of prerequisites
```

Nodes with:

```text
inDegree == 0
```

are ready to process.

This is the core of:

```text
Kahn's Algorithm
```

Pattern:

```text
Find In-degree 0
       ↓
Process Node
       ↓
Remove Its Edges
       ↓
Decrease Neighbor In-degree
       ↓
New In-degree 0 Nodes
```

#### 6. Kahn's Algorithm Logic — Must Know

```kotlin
for (node in 0 until n) {
    if (indegree[node] == 0) {
        queue.addLast(node)
    }
}

while (queue.isNotEmpty()) {

    val node = queue.removeFirst()

    for (neighbor in graph[node]) {

        indegree[neighbor]--

        if (indegree[neighbor] == 0) {
            queue.addLast(neighbor)
        }
    }
}
```

#### 7. Cycle Detection Pattern — Must Know

After Kahn's Algorithm:

```text
processed == V
      ↓
No Cycle
```

If:

```text
processed < V
      ↓
Cycle Exists
```

Why?

Nodes inside a dependency cycle never reach:

```text
inDegree = 0
```

#### 8. Common In-degree Patterns — Must Know

1. **Course prerequisites**
   ```text
   In-degree = remaining prerequisites
   ```

2. **Task scheduling**
   ```text
   In-degree = unfinished dependencies
   ```

3. **Topological Sort**
   ```text
   Start with In-degree 0
   ```

4. **Cycle detection**
   ```text
   processed < V
   ```

5. **Find starting/source nodes**
   ```text
   In-degree = 0
   ```

#### 9. Common Out-degree Patterns — Good to Know

Out-degree is useful for finding:

1. Terminal/sink nodes.

```text
outDegree == 0
```

2. Nodes with no outgoing dependency.

3. Graph problems processed **backwards**.

4. Reverse-graph patterns such as eventual safe states.

Example:

```text
A → B → C
```

`C`:

```text
outDegree = 0
```

so `C` is a terminal node.

#### 10. Reverse Graph Pattern — Good to Know

Sometimes a problem becomes easier by reversing edges.

Original:

```text
A → B
```

Reverse:

```text
B → A
```

Then original:

```text
outDegree
```

can behave like:

```text
inDegree
```

in the reversed graph.

This allows Kahn-style processing from terminal nodes.

#### 11. Important Property — Good to Know

For any directed graph:

```text
Sum of In-degrees = E

Sum of Out-degrees = E
```

Therefore:

```text
Sum of In-degrees
=
Sum of Out-degrees
=
Number of Edges
```

Useful as a basic graph property/check.

#### 12. Undirected Graph Degree

For an undirected graph:

```text
A — B
```

we normally just say:

```text
Degree
```

not in-degree/out-degree.

Important property:

```text
Sum of Degrees = 2E
```

because every edge touches two vertices.

#### 13. Complexity — Must Know

Calculating all degrees:

```text
Time  → O(V + E)
Space → O(V)
```

If only processing an edge list:

```text
Time → O(E)
```

Degree arrays:

```text
Space → O(V)
```

#### 14. Common Mistakes — Must Know

1. Mixing up incoming and outgoing edges.
2. For `u → v`, incrementing `indegree[u]` instead of `indegree[v]`.
3. Treating undirected graphs as having in/out-degree.
4. Forgetting to decrement in-degree during Kahn's Algorithm.
5. Assuming there is only one in-degree `0` node.
6. Assuming every graph has an in-degree `0` node — a directed cycle may have none.

#### 15. Interview Must Remember

1. `In-degree` → **incoming edges**.
2. `Out-degree` → **outgoing edges**.
3. For `u → v`:

```text
outDegree[u]++
inDegree[v]++
```

4. `inDegree == 0` → source / no remaining prerequisite.
5. `outDegree == 0` → sink / terminal node.
6. **Kahn's Algorithm heavily depends on in-degree**.
7. `processed < V` in Kahn → **cycle exists**.
8. Directed graph → `Σ in-degree = Σ out-degree = E`.