# Quickselect

#### 1. Definition — Good to Know

Quickselect finds the **Kth smallest or Kth largest element** without fully sorting the array.

It uses the same **partition idea as Quicksort**.

#### 2. Why It Is Used

Instead of sorting everything:

```text
Sort → O(N log N)
```

Quickselect can find a Kth element in:

```text
Average → O(N)
```

Example:

```text
Array = [7, 2, 5, 1, 9]
K = 3rd smallest

Answer = 5
```

#### 3. Core Idea — Must Know

Choose a pivot and partition the array:

```text
Smaller values | Pivot | Larger values
```

After partitioning, the pivot is at its **final sorted position**.

Then:

```text
pivotIndex == target → Found

pivotIndex > target  → Search Left

pivotIndex < target  → Search Right
```

Unlike Quicksort, Quickselect explores only **one side**.

#### 4. Kth Smallest Index

For:

```text
Kth smallest
```

target index is:

```text
k - 1
```

Example:

```text
3rd smallest → index 2
```

#### 5. Kth Largest Index — Must Know

For an array of size `N`:

```text
Kth largest → index N - K
```

Example:

```text
N = 5
K = 2

Target index = 5 - 2 = 3
```

#### 6. Algorithm

```text
1. Choose a pivot.

2. Partition the array.

3. Get pivotIndex.

4. Compare pivotIndex with targetIndex.

5. Search only the required side.

6. Stop when pivotIndex == targetIndex.
```

#### 7. Kotlin Implementation

Example: **Kth largest element**.

```kotlin
fun findKthLargest(nums: IntArray, k: Int): Int {

    val target = nums.size - k

    var left = 0
    var right = nums.lastIndex

    while (left <= right) {

        val pivotIndex = partition(nums, left, right)

        when {
            pivotIndex == target -> return nums[pivotIndex]
            pivotIndex < target -> left = pivotIndex + 1
            else -> right = pivotIndex - 1
        }
    }

    return -1
}

fun partition(nums: IntArray, left: Int, right: Int): Int {

    val pivot = nums[right]
    var index = left

    for (i in left until right) {

        if (nums[i] <= pivot) {
            nums[i] = nums[index].also {
                nums[index] = nums[i]
            }
            index++
        }
    }

    nums[index] = nums[right].also {
        nums[right] = nums[index]
    }

    return index
}
```

#### 8. Time & Space Complexity — Must Know

```text
Average Time → O(N)
Worst Time   → O(N²)

Iterative Extra Space → O(1)
```

Worst case happens when poor pivots repeatedly create very unbalanced partitions.

A **random pivot** helps reduce this risk in practice.

#### 9. Quickselect vs Sorting

```text
Need complete sorted order
        ↓
      Sorting


Need only Kth element
        ↓
    Quickselect
```

Typical:

```text
Sorting     → O(N log N)
Quickselect → O(N) average
```

#### 10. Quickselect vs Heap — Good to Know

For Kth largest/smallest:

**Quickselect**

```text
Average → O(N)
Modifies array
Good for one-time selection
```

**Heap**

```text
O(N log K)
Useful for streaming / repeated processing
Doesn't require partitioning the input
```

#### 11. Common Interview Problems

1. Kth largest element.
2. Kth smallest element.
3. Find median / order statistic.
4. Select an element by rank.

#### 12. Edge Cases / Common Mistakes

1. `k = 1`.
2. `k = N`.
3. Duplicate values.
4. Confusing Kth smallest with Kth largest index.
5. Partition implementation errors.
6. Forgetting Quickselect modifies the array.
7. Assuming worst-case complexity is `O(N)`.

#### 13. Interview Must Remember

1. Quickselect → **Kth smallest/largest without full sorting**.
2. Uses **partitioning like Quicksort**.
3. Search only **one partition** after each step.
4. Kth smallest index → `k - 1`.
5. Kth largest index → `N - k`.
6. Average → **`O(N)`**, worst → **`O(N²)`**.
7. Randomized pivot helps avoid consistently bad partitions.