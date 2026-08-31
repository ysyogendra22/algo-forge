
#### 1. How it works
1. Divide the array into two halves.
2. Keep dividing until each part has one element.
3. Merge the smaller parts in sorted order.
4. Continue merging until the complete array is sorted.

#### 2. Complexity
1. Best: O(n log n)
2. Average: O(n log n)
3. Worst: O(n log n)
4. Space: O(n)

#### 3. Implementation - Kotlin
```

fun mergeSort(arr: IntArray) {
    if (arr.size <= 1) return

    val mid = arr.size / 2
    val left = arr.copyOfRange(0, mid)
    val right = arr.copyOfRange(mid, arr.size)

    mergeSort(left)
    mergeSort(right)

    merge(arr, left, right)
}

fun merge(arr: IntArray, left: IntArray, right: IntArray) {
    var i = 0
    var j = 0
    var k = 0

    while (i < left.size && j < right.size) {
        if (left[i] <= right[j]) {
            arr[k++] = left[i++]
        } else {
            arr[k++] = right[j++]
        }
    }

    while (i < left.size) {
        arr[k++] = left[i++]
    }

    while (j < right.size) {
        arr[k++] = right[j++]
    }
}

```
#### 4. When to use
1. Large datasets.
2. When guaranteed O(n log n) performance is required.
3. When stable sorting is required.
4. Good for linked lists.
5. Useful for external sorting of very large data.

#### 5. Trade-offs
1. Guaranteed O(n log n) performance.
2. Stable sorting.
3. Good for large datasets.
4. Requires O(n) extra space for arrays.
5. Usually not in-place for arrays.
6. More memory usage than Quick Sort.