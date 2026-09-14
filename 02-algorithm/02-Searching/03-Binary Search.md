# Binary Search

#### 1. Definition — Must Know

Binary Search finds a target by repeatedly **dividing the search space in half**.

For standard Binary Search, the array must be **sorted**.

#### 2. Why It Is Used

1. Searches sorted data efficiently.
2. Eliminates half of the remaining elements at every step.
3. Reduces search time from `O(N)` to `O(log N)`.

#### 3. How It Works

Example:

```text id="bs01"
Array  = [10, 20, 30, 40, 50, 60, 70]
Target = 60
```

First:

```text id="bs02"
[10, 20, 30, 40, 50, 60, 70]
             ↑
            mid = 40
```

`60 > 40`, so discard the left half.

```text id="bs03"
[50, 60, 70]
     ↑
   Found
```

#### 4. Core Concepts — Must Know

1. **Left** — beginning of current search space.
2. **Right** — end of current search space.
3. **Mid** — middle position.
4. If `target < nums[mid]` → search left half.
5. If `target > nums[mid]` → search right half.
6. If equal → target found.

#### 5. Algorithm — Must Know

```text id="bs04"
left = 0
right = n - 1

while left <= right:

    mid = left + (right - left) / 2

    if nums[mid] == target:
        return mid

    if target < nums[mid]:
        right = mid - 1

    else:
        left = mid + 1

return -1
```

#### 6. Kotlin Implementation — Must Know

```kotlin id="bs05"
fun binarySearch(nums: IntArray, target: Int): Int {

    var left = 0
    var right = nums.lastIndex

    while (left <= right) {

        val mid = left + (right - left) / 2

        when {
            nums[mid] == target -> return mid
            target < nums[mid] -> right = mid - 1
            else -> left = mid + 1
        }
    }

    return -1
}
```

#### 7. Time & Space Complexity — Must Know

| Case | Time |
|---|---:|
| Best | `O(1)` |
| Average | `O(log N)` |
| Worst | `O(log N)` |
| Space | `O(1)` |

Why `O(log N)`?

```text id="bs06"
N → N/2 → N/4 → N/8 → ...
```

The search space is halved each time.

#### 8. Common Binary Search Patterns — Must Know

1. Exact target search.
2. First / last occurrence.
3. Lower Bound / Upper Bound.
4. Search in rotated sorted array.
5. Search in 2D matrix.
6. Binary Search on Answer.

Study these patterns separately.

#### 9. Edge Cases / Common Mistakes

1. Empty array.
2. Single element.
3. Target not present.
4. Target at first or last position.
5. Duplicate values.
6. Using Binary Search on unsorted data.
7. Wrong `left` / `right` updates causing infinite loops.
8. Using the wrong loop condition.

#### 10. When to Use / When Not to Use

**Use when:**

1. Data is sorted.
2. Search space has a clear **monotonic property**.
3. You can eliminate half of the search space after each decision.

**Avoid when:**

1. Data is unsorted and cannot be searched using a monotonic condition.
2. Only sequential access is available.

#### 11. Related Topics

1. First / Last Occurrence
2. Lower Bound / Upper Bound
3. Rotated Sorted Array
4. Binary Search on Answer

#### 12. Interview Must Remember

1. Standard Binary Search requires **sorted data**.
2. Core idea → **eliminate half of the search space**.
3. Time → `O(log N)`.
4. Iterative space → `O(1)`.
5. Use:

```kotlin id="bs07"
val mid = left + (right - left) / 2
```

6. Most Binary Search bugs come from **boundary conditions**.