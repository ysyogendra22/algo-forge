# Search in 2D Matrix

#### 1. Definition — Must Know

Search for a target value inside a **sorted 2D matrix**.

Example:

```text
1   3   5   7
10  11  16  20
23  30  34  60

Target = 16
```

Result:

```text
Found
```

#### 2. Important Property — Must Know

For the standard Binary Search matrix problem:

1. Each row is sorted.
2. First element of each row is greater than the last element of the previous row.

```text
1  3  5  7 | 10  11  16  20 | 23  30  34  60
```

So the matrix can be treated as **one sorted array**.

#### 3. Core Idea — Must Know

Instead of creating a new array, treat the matrix virtually as:

```text
[1, 3, 5, 7, 10, 11, 16, 20, 23, 30, 34, 60]
```

If:

```text
rows = m
columns = n
```

Total elements:

```text
m × n
```

Binary Search range:

```text
left  = 0
right = (m × n) - 1
```

#### 4. Convert 1D Index to 2D — Must Know

For a virtual index `mid`:

```text
row = mid / columns
col = mid % columns
```

Then:

```text
matrix[row][col]
```

Example with `4` columns:

```text
mid = 6

row = 6 / 4 = 1
col = 6 % 4 = 2

matrix[1][2] = 16
```

#### 5. Algorithm — Must Know

```text
1. Treat matrix as a virtual sorted array.

2. left = 0
   right = rows * cols - 1

3. Find mid.

4. Convert mid:
   row = mid / cols
   col = mid % cols

5. Compare matrix[row][col] with target.

6. Move left or right like normal Binary Search.
```

#### 6. Kotlin Implementation — Must Know

```kotlin
fun searchMatrix(matrix: Array<IntArray>, target: Int): Boolean {

    if (matrix.isEmpty() || matrix[0].isEmpty()) {
        return false
    }

    val rows = matrix.size
    val cols = matrix[0].size

    var left = 0
    var right = rows * cols - 1

    while (left <= right) {

        val mid = left + (right - left) / 2

        val row = mid / cols
        val col = mid % cols

        val value = matrix[row][col]

        when {
            value == target -> return true
            value < target -> left = mid + 1
            else -> right = mid - 1
        }
    }

    return false
}
```

#### 7. Time & Space Complexity — Must Know

There are:

```text
M × N
```

elements.

Binary Search:

```text
Time  → O(log(M × N))
Space → O(1)
```

#### 8. Another 2D Matrix Pattern — Good to Know

Sometimes the matrix has a different property:

```text
Each row    → sorted
Each column → sorted
```

Example:

```text
1   4   7
2   5   8
3   6   9
```

But the entire matrix cannot be treated as one sorted array.

Use **Staircase Search**:

```text
Start → Top Right

Target < current → Move Left
Target > current → Move Down
```

Complexity:

```text
O(M + N)
```

This is a different matrix-search pattern.

#### 9. Edge Cases / Common Mistakes

1. Empty matrix.
2. Single row.
3. Single column.
4. Target not present.
5. Target at first or last position.
6. Incorrect `row / col` conversion.
7. Assuming every row-and-column sorted matrix can be flattened for Binary Search.

#### 10. Interview Must Remember

1. First understand **how the matrix is sorted**.
2. Fully ordered matrix → treat as a virtual 1D sorted array.
3. `row = mid / cols`.
4. `col = mid % cols`.
5. Binary Search → **`O(log(M × N))`**.
6. Row + column sorted only → consider **Staircase Search `O(M + N)`**.