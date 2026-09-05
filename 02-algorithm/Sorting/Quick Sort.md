#### 1. How it works
1. Choose an element as a pivot.
2. Put smaller elements before the pivot.
3. Put larger elements after the pivot.
4. Pivot reaches its correct position.
5. Repeat the same process for left and right parts.

#### 2. Complexity
1. Best: O(n log n)
2. Average: O(n log n)
3. Worst: O(n²)
4. Space: O(log n) average due to recursion

#### 3. Implementation - Kotlin
```

fun quickSort(arr: IntArray, low: Int = 0, high: Int = arr.lastIndex) {
    if (low < high) {
        val pivotIndex = partition(arr, low, high)

        quickSort(arr, low, pivotIndex - 1)
        quickSort(arr, pivotIndex + 1, high)
    }
}

fun partition(arr: IntArray, low: Int, high: Int): Int {
    val pivot = arr[high]
    var i = low - 1

    for (j in low until high) {
        if (arr[j] <= pivot) {
            i++

            val temp = arr[i]
            arr[i] = arr[j]
            arr[j] = temp
        }
    }

    val temp = arr[i + 1]
    arr[i + 1] = arr[high]
    arr[high] = temp

    return i + 1
}

```

#### 4. When to use
1. Large arrays.
2. Good for general-purpose in-memory sorting.
3. Useful when low extra memory is important.
4. Good when average performance matters more than worst-case guarantee.
5. Avoid simple pivot selection when data may already be sorted.

#### 5. Trade-offs
1. Average performance is O(n log n).
2. Usually fast in practice for arrays.
3. Can mostly sort in-place.
4. Usually not stable.
5. Worst case is O(n²).
6. Pivot selection strongly affects performance.
7. Uses less extra memory than Merge Sort for arrays.