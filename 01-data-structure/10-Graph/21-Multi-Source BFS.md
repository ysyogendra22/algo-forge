# Multi-Source BFS

#### 1. Definition — Must Know

1. **Multi-Source BFS** is BFS that starts from **multiple source nodes at the same time**.
2. Add all source nodes to the queue initially.
3. Then run normal BFS.
4. Used to find the minimum distance/time from the **nearest source**.

```text
Single-Source BFS:

Queue → [S]


Multi-Source BFS:

Queue → [S1, S2, S3]
```

#### 2. Why It Is Used — Must Know

Use it when multiple locations start with the **same initial state/time**.

Examples:

1. Rotting Oranges → multiple rotten oranges spread simultaneously.
2. Distance to nearest `0`.
3. Distance to nearest gate.
4. Fire/infection spreading from multiple locations.
5. Nearest source in an unweighted graph.

Think:

```text
Multiple Sources + Minimum Distance/Time
                ↓
         Multi-Source BFS
```

#### 3. How It Works — Must Know

Example:

```text
S . . . S
. . . . .
. . X . .
```

Both `S` nodes start at:

```text
Distance = 0
```

Initial queue:

```text
[S1, S2]
```

BFS expands from both simultaneously:

```text
Level 0 → Sources
Level 1 → Their neighbors
Level 2 → Next neighbors
...
```

Therefore, each node is reached from its **nearest source**.

#### 4. Core Logic — Must Know

```text
1. Find all source nodes.

2. Add ALL sources to Queue.

3. Mark all sources visited / distance = 0.

4. Run normal BFS.

5. For every unvisited neighbor:

   distance[neighbor] =
       distance[current] + 1

   add neighbor to Queue.
```

The important difference from normal BFS is only the **initialization**.

#### 5. Kotlin Implementation — Must Know

```kotlin
fun multiSourceBfs(
    n: Int,
    graph: Array<MutableList<Int>>,
    sources: List<Int>
): IntArray {

    val distance = IntArray(n) { -1 }
    val queue = ArrayDeque<Int>()

    for (source in sources) {
        distance[source] = 0
        queue.addLast(source)
    }

    while (queue.isNotEmpty()) {

        val node = queue.removeFirst()

        for (neighbor in graph[node]) {

            if (distance[neighbor] == -1) {

                distance[neighbor] =
                    distance[node] + 1

                queue.addLast(neighbor)
            }
        }
    }

    return distance
}
```

Here:

```text
distance[node] == -1 → Unvisited
```

#### 6. Grid Pattern — Must Know

This pattern appears very often with grids.

Example:

```text
2 1 1
1 1 0
0 1 2
```

Suppose:

```text
2 → Source
1 → Can be reached
0 → Blocked
```

Initial queue:

```text
[(0,0), (2,2)]
```

Both sources spread simultaneously.

#### 7. Rotting Oranges Pattern — Must Know

Instead of running BFS separately from every rotten orange:

```text
Wrong idea:

BFS(source1)
BFS(source2)
BFS(source3)
```

Do:

```text
Queue = [source1, source2, source3]

Run ONE BFS
```

Why?

All rotten oranges start spreading at the **same time**.

Each BFS level represents:

```text
1 unit of time
```

#### 8. Why Not Run BFS Separately? — Must Know

Running BFS from every source independently can repeat the same work.

Multi-source BFS:

```text
All Sources
     ↓
One BFS
     ↓
Each Node Processed Once
```

This is both simpler and more efficient.

#### 9. Time & Space Complexity — Must Know

Graph:

```text
Time  → O(V + E)
Space → O(V)
```

Grid with `R × C` cells:

```text
Time  → O(R × C)
Space → O(R × C)
```

Adding multiple sources does **not** change the overall BFS complexity.

#### 10. Multi-Source BFS vs Single-Source BFS — Must Know

```text
Single-Source BFS            Multi-Source BFS

One initial source           Multiple initial sources
Queue = [S]                  Queue = [S1,S2,S3]
Distance from S              Distance from nearest source
Normal BFS afterward         Normal BFS afterward
```

The traversal logic is essentially the same.

#### 11. Common Interview Patterns — Must Know

1. **Multiple sources spreading**
   ```text
   Multi-Source BFS
   ```

2. **Nearest source**
   ```text
   Multi-Source BFS
   ```

3. **Minimum time to spread**
   ```text
   BFS Levels
   ```

4. **Distance from nearest special cell**
   ```text
   Initialize all special cells as sources
   ```

Common examples:

```text
Rotting Oranges
01 Matrix
Walls and Gates
Fire / Infection Spread
```

#### 12. Common Mistakes — Must Know

1. Running separate BFS from every source.
2. Adding sources gradually instead of putting **all sources in the initial queue**.
3. Forgetting to mark initial sources visited.
4. Counting the initial level as `1` instead of `0`.
5. Forgetting unreachable cells/nodes.
6. Using DFS when the problem asks for minimum distance/time in an unweighted graph.

#### 13. Interview Must Remember

1. Multi-Source BFS = **normal BFS with multiple starting nodes**.
2. Add **all sources to the queue initially**.
3. All sources start at `distance = 0`.
4. BFS gives distance from the **nearest source**.
5. Spread/time problems → each BFS level can represent one time unit.
6. Graph complexity → `O(V + E)`.
7. **Multiple sources + minimum distance/time → think Multi-Source BFS**.