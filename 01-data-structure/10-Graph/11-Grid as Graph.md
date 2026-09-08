# Grid as Graph

#### 1. Definition — Must Know

1. A **2D grid can be treated as a graph**.
2. Each cell → **Vertex / Node**.
3. Valid movement between cells → **Edge**.
4. Then normal graph algorithms like **DFS and BFS** can be applied.

```text
Grid:

1 1 0
0 1 1
0 0 1
```

Each cell is a node connected to allowed neighboring cells.

#### 2. Why It Is Used — Must Know

Many interview problems are given as matrices but are actually graph problems.

Examples:

1. Number of Islands.
2. Flood Fill.
3. Rotting Oranges.
4. Shortest Path in a Grid.
5. Maze problems.
6. Surrounded Regions.

Think:

```text
Grid + Movement = Graph
```

#### 3. Neighbor Directions — Must Know

Most problems allow movement in **4 directions**:

```text
       Up
        ↑
Left ← Cell → Right
        ↓
       Down
```

Directions:

```text
(-1, 0) → Up
( 1, 0) → Down
( 0,-1) → Left
( 0, 1) → Right
```

Kotlin:

```kotlin
val directions = arrayOf(
    intArrayOf(-1, 0),
    intArrayOf(1, 0),
    intArrayOf(0, -1),
    intArrayOf(0, 1)
)
```

#### 4. 8-Direction Movement — Good to Know

Some problems also allow diagonals.

```text
↖ ↑ ↗
← X →
↙ ↓ ↘
```

That gives **8 neighbors**.

Always read the movement rules before implementing traversal.

#### 5. DFS on Grid — Must Know

```kotlin
fun dfs(
    row: Int,
    col: Int,
    grid: Array<CharArray>
) {
    if (
        row !in grid.indices ||
        col !in grid[0].indices ||
        grid[row][col] != '1'
    ) {
        return
    }

    grid[row][col] = '0'

    dfs(row - 1, col, grid)
    dfs(row + 1, col, grid)
    dfs(row, col - 1, grid)
    dfs(row, col + 1, grid)
}
```

Pattern:

```text
Check Boundary
      ↓
Check Valid Cell
      ↓
Mark Visited
      ↓
Explore Neighbors
```

#### 6. BFS on Grid — Must Know

```kotlin
fun bfs(
    startRow: Int,
    startCol: Int,
    grid: Array<CharArray>
) {
    val queue = ArrayDeque<Pair<Int, Int>>()

    queue.addLast(startRow to startCol)
    grid[startRow][startCol] = '0'

    val directions = arrayOf(
        intArrayOf(-1, 0),
        intArrayOf(1, 0),
        intArrayOf(0, -1),
        intArrayOf(0, 1)
    )

    while (queue.isNotEmpty()) {

        val (row, col) = queue.removeFirst()

        for ((dr, dc) in directions) {

            val newRow = row + dr
            val newCol = col + dc

            if (
                newRow in grid.indices &&
                newCol in grid[0].indices &&
                grid[newRow][newCol] == '1'
            ) {
                grid[newRow][newCol] = '0'
                queue.addLast(newRow to newCol)
            }
        }
    }
}
```

#### 7. Visited Tracking — Must Know

Two common approaches:

**Separate visited array:**

```kotlin
val visited = Array(rows) {
    BooleanArray(cols)
}
```

Or modify the grid itself:

```kotlin
grid[row][col] = '0'
```

Modifying the grid is simpler when the problem allows it.

#### 8. Number of Islands Pattern — Must Know

```text
1 1 0 0
1 0 0 1
0 0 1 1
```

Logic:

```text
For every cell:

    if cell == land:
        islands++
        DFS/BFS to mark entire island
```

One DFS/BFS discovers **one connected component**.

So:

```text
Island = Connected Component
```

#### 9. Shortest Path Pattern — Must Know

If every movement has equal cost:

```text
Grid + Minimum Steps
        ↓
       BFS
```

Why?

BFS explores:

```text
Distance 0
Distance 1
Distance 2
Distance 3
...
```

So the first time the destination is reached gives the minimum number of moves.

#### 10. Multi-Source BFS — Good to Know

Sometimes multiple cells are starting points.

Example:

```text
Rotting Oranges
```

Instead of starting BFS from one cell:

```text
Add ALL starting cells to queue
        ↓
Run BFS together
```

Pattern:

```text
Multiple sources + minimum time/distance
                ↓
         Multi-Source BFS
```

#### 11. Time & Space Complexity — Must Know

For:

```text
Rows = R
Columns = C
```

Total cells:

```text
V = R × C
```

Each cell has at most a constant number of neighbors.

Therefore:

```text
Time  → O(R × C)
Space → O(R × C)
```

DFS recursion or BFS queue can contain up to `R × C` cells.

#### 12. Common Patterns — Must Know

1. **Connected Areas**
   ```text
   DFS / BFS
   ```

2. **Number of Islands**
   ```text
   Connected Components
   ```

3. **Flood Fill**
   ```text
   DFS / BFS
   ```

4. **Minimum Steps / Shortest Path**
   ```text
   BFS
   ```

5. **Multiple Starting Points**
   ```text
   Multi-Source BFS
   ```

6. **Path Exploration**
   ```text
   DFS / Backtracking
   ```

#### 13. Common Mistakes — Must Know

1. Forgetting row/column boundary checks.
2. Forgetting to mark cells visited.
3. Marking BFS cells visited too late.
4. Assuming diagonal movement when only 4 directions are allowed.
5. Using DFS for minimum-step problems when BFS is simpler.
6. Modifying the original grid when the problem requires preserving it.

#### 14. Interview Must Remember

1. **Cell = Vertex, movement = Edge**.
2. Grid problems are often graph problems in disguise.
3. Connected region → think **DFS/BFS**.
4. Minimum steps → think **BFS**.
5. Multiple sources → think **Multi-Source BFS**.
6. Always check **boundaries + visited + valid cell**.
7. Typical complexity → `O(R × C)`.