# Flood Fill Pattern

#### 1. Definition — Must Know

1. **Flood Fill** starts from one cell and visits all connected cells having the same valid state/value.
2. It is essentially **DFS/BFS on a grid**.
3. Commonly used to modify or identify a connected region.

Think:

```text
Start Cell → Explore Connected Same-Value Cells → Mark/Change Them
```

#### 2. Example — Must Know

Input:

```text
1 1 1
1 1 0
1 0 1
```

Start at `(1,1)` and change `1 → 2`.

Result:

```text
2 2 2
2 2 0
2 0 1
```

The bottom-right `1` remains unchanged because it is **not connected** to the starting region.

#### 3. Core Logic — Must Know

```text
1. Get starting cell's original value.
2. Change the current cell.
3. Explore its neighbors.
4. Continue only if neighbor has the original value.
5. Stop at boundary or different-value cells.
```

Pattern:

```text
Validate → Mark → Explore Neighbors
```

#### 4. DFS Implementation — Must Know

```kotlin
fun floodFill(
    image: Array<IntArray>,
    sr: Int,
    sc: Int,
    color: Int
): Array<IntArray> {

    val original = image[sr][sc]

    if (original == color) return image

    fun dfs(row: Int, col: Int) {

        if (
            row !in image.indices ||
            col !in image[0].indices ||
            image[row][col] != original
        ) {
            return
        }

        image[row][col] = color

        dfs(row - 1, col)
        dfs(row + 1, col)
        dfs(row, col - 1)
        dfs(row, col + 1)
    }

    dfs(sr, sc)

    return image
}
```

#### 5. Why `original == color` Check Matters — Must Know

Without:

```kotlin
if (original == color) return image
```

changing the cell does not mark it differently.

Example:

```text
Original = 1
New      = 1
```

DFS can repeatedly revisit the same cells.

#### 6. BFS Alternative — Good to Know

```kotlin
val queue = ArrayDeque<Pair<Int, Int>>()

queue.addLast(sr to sc)
image[sr][sc] = color

while (queue.isNotEmpty()) {

    val (row, col) = queue.removeFirst()

    for ((dr, dc) in directions) {

        val nr = row + dr
        val nc = col + dc

        if (
            nr in image.indices &&
            nc in image[0].indices &&
            image[nr][nc] == original
        ) {
            image[nr][nc] = color
            queue.addLast(nr to nc)
        }
    }
}
```

Both DFS and BFS work.

#### 7. Time & Space Complexity — Must Know

For:

```text
Rows = R
Columns = C
```

Worst case:

```text
Time  → O(R × C)
Space → O(R × C)
```

Every cell may need to be visited once.

#### 8. Common Flood Fill Patterns — Must Know

1. **Recolor Connected Region**
   ```text
   Flood Fill
   ```

2. **Count Islands**
   ```text
   Find land → Flood Fill → count++
   ```

3. **Mark Visited Region**
   ```text
   Valid Cell → DFS/BFS → mark entire component
   ```

4. **Surrounded Regions**
   ```text
   Flood Fill from boundary cells
   ```

5. **Area of Island**
   ```text
   Flood Fill + count visited cells
   ```

#### 9. Flood Fill vs Connected Components — Must Know

Flood Fill:

```text
Start from a known cell
        ↓
Explore its entire connected region
```

Connected Components:

```text
Check every cell
      ↓
For each unvisited valid cell
      ↓
Run Flood Fill
      ↓
Count++
```

So **Flood Fill is often the operation used to discover one connected component**.

#### 10. Common Mistakes — Must Know

1. Forgetting boundary checks.
2. Exploring cells with a different original value.
3. Forgetting `original == newColor`.
4. Marking visited **after** recursive calls instead of before.
5. Assuming diagonal movement without checking the problem.
6. Using a separate `visited` array when modifying the grid itself is allowed and sufficient.

#### 11. Interview Must Remember

1. Flood Fill = **DFS/BFS over one connected grid region**.
2. Store the **original value** before traversal.
3. Pattern → `Validate → Mark → Explore`.
4. Changing the cell can act as the `visited` marker.
5. `original == newColor` is an important edge case.
6. Complexity → `O(R × C)`.
7. Islands, regions, and connected-area problems often use the same pattern.