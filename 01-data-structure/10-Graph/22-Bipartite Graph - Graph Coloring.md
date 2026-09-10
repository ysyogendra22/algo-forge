# Bipartite Graph / Graph Coloring

#### 1. Definition — Must Know

1. A **Bipartite Graph** can divide its vertices into **two groups**.
2. Every edge must connect vertices from **different groups**.
3. No edge can connect two vertices in the same group.
4. Think of it as coloring the graph using exactly **2 colors**.

```text id="bp01"
Color A → 0
Color B → 1
```

#### 2. Example — Must Know

Bipartite:

```text id="bp02"
A ----- B
|       |
D ----- C
```

Possible coloring:

```text id="bp03"
A → Red
B → Blue
C → Red
D → Blue
```

Every connected edge has different colors.

#### 3. Non-Bipartite Example — Must Know

```text id="bp04"
    A
   / \
  B---C
```

Try coloring:

```text id="bp05"
A → Red
B → Blue
C → Blue
```

But:

```text id="bp06"
B ----- C
```

connects two Blue vertices.

Therefore the graph is **not bipartite**.

#### 4. Important Rule — Must Know

An undirected graph is bipartite **if and only if it contains no odd-length cycle**.

```text id="bp07"
Even Cycle → Can be Bipartite

Odd Cycle  → Not Bipartite
```

Example:

```text id="bp08"
Triangle = 3 edges
          ↓
      Odd Cycle
          ↓
    Not Bipartite
```

This is one of the most important interview facts.

#### 5. Core Logic — Must Know

Use:

```text id="bp09"
BFS/DFS + Color Array
```

Color states:

```text id="bp10"
-1 → Not colored
 0 → Color A
 1 → Color B
```

For every edge:

```text id="bp11"
u ----- v

color[u] != color[v]
```

If both have the same color:

```text id="bp12"
Same Color
    ↓
Not Bipartite
```

#### 6. BFS Algorithm — Must Know

```text id="bp13"
1. Pick an uncolored node.

2. Assign color 0.

3. Add it to Queue.

4. For every neighbor:

   if uncolored:
       assign opposite color
       add to Queue

   else if same color:
       return false

5. Repeat for every disconnected component.
```

Opposite color:

```text id="bp14"
1 - color[node]
```

#### 7. Kotlin BFS Implementation — Must Know

```kotlin id="bp15"
fun isBipartite(
    graph: Array<IntArray>
): Boolean {

    val color = IntArray(graph.size) { -1 }

    for (start in graph.indices) {

        if (color[start] != -1) continue

        val queue = ArrayDeque<Int>()

        queue.addLast(start)
        color[start] = 0

        while (queue.isNotEmpty()) {

            val node = queue.removeFirst()

            for (neighbor in graph[node]) {

                if (color[neighbor] == -1) {

                    color[neighbor] = 1 - color[node]
                    queue.addLast(neighbor)

                } else if (color[neighbor] == color[node]) {

                    return false
                }
            }
        }
    }

    return true
}
```

#### 8. DFS Implementation — Good to Know

```kotlin id="bp16"
fun isBipartite(
    graph: Array<IntArray>
): Boolean {

    val color = IntArray(graph.size) { -1 }

    fun dfs(node: Int, currentColor: Int): Boolean {

        color[node] = currentColor

        for (neighbor in graph[node]) {

            if (color[neighbor] == -1) {

                if (!dfs(neighbor, 1 - currentColor)) {
                    return false
                }

            } else if (color[neighbor] == currentColor) {

                return false
            }
        }

        return true
    }

    for (node in graph.indices) {

        if (color[node] == -1) {

            if (!dfs(node, 0)) {
                return false
            }
        }
    }

    return true
}
```

#### 9. Disconnected Graph — Must Know

Graph:

```text id="bp17"
0 --- 1       2 --- 3
```

One BFS/DFS may not cover every component.

Therefore:

```kotlin id="bp18"
for (node in graph.indices) {

    if (color[node] == -1) {
        // Start BFS/DFS
    }
}
```

Every component must satisfy the coloring rule.

#### 10. Time & Space Complexity — Must Know

```text id="bp19"
Time  → O(V + E)
Space → O(V)
```

1. Every vertex is colored once.
2. Every edge is examined.
3. Color array + BFS queue/DFS stack → `O(V)`.

#### 11. Common Interview Patterns — Must Know

1. **Can graph be divided into two groups?**
   ```text
   Bipartite Check
   ```

2. **Two-team assignment with conflicts**
   ```text
   Bipartite Graph
   ```

3. **People who dislike each other into two groups**
   ```text
   Bipartite Graph
   ```

4. **2-color graph**
   ```text
   BFS/DFS + Coloring
   ```

5. **Odd cycle exists**
   ```text
   Not Bipartite
   ```

#### 12. General Graph Coloring — Good to Know

Bipartite checking is specifically:

```text id="bp20"
2-Coloring
```

General graph coloring asks:

```text id="bp21"
Can we color the graph using K colors
so adjacent nodes have different colors?
```

Example:

```text id="bp22"
Triangle:

A
|\
| \
B--C
```

Requires at least:

```text id="bp23"
3 colors
```

For FAANG preparation:

```text id="bp24"
Bipartite / 2-Coloring → Must Know

General K-Coloring     → Good to Know

Advanced coloring algorithms
                      → Low Priority
```

#### 13. Common Mistakes — Must Know

1. Checking only one connected component.
2. Forgetting to assign the opposite color.
3. Using only `visited` instead of tracking colors.
4. Assuming every cyclic graph is non-bipartite.
5. **Even cycles can be bipartite; odd cycles cannot.**
6. A self-loop immediately makes a graph non-bipartite.

#### 14. Interview Must Remember

1. Bipartite = graph can be divided into **2 groups**.
2. Adjacent vertices must have **different colors**.
3. Solve using **BFS/DFS + 2-coloring**.
4. Opposite color → `1 - color[node]`.
5. Same-colored neighbors → **not bipartite**.
6. **Odd cycle → not bipartite**.
7. Complexity → `O(V + E)`.