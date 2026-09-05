#### 1. How it works

1. Convert the array into a Max Heap.
2. Largest element stays at the root.
3. Swap the root with the last element.
4. Reduce the heap size.
5. Heapify again and repeat until sorted.

#### 2. Complexity

1. Best: O(n log n)
2. Average: O(n log n)
3. Worst: O(n log n)
4. Space: O(1)

#### 3. Implementation - Kotlin

```

fun heapSort(arr: IntArray) {
    val n = arr.size

    // Build Max Heap
    for (i in n / 2 - 1 downTo 0) {
        heapify(arr, n, i)
    }

    // Move largest element to the end
    for (i in n - 1 downTo 1) {
        val temp = arr[0]
        arr[0] = arr[i]
        arr[i] = temp

        heapify(arr, i, 0)
    }
}

fun heapify(arr: IntArray, size: Int, root: Int) {
    var largest = root
    val left = 2 * root + 1
    val right = 2 * root + 2

    if (left < size && arr[left] > arr[largest]) {
        largest = left
    }

    if (right < size && arr[right] > arr[largest]) {
        largest = right
    }

    if (largest != root) {
        val temp = arr[root]
        arr[root] = arr[largest]
        arr[largest] = temp

        heapify(arr, size, largest)
    }
}

```

#### 4. When to use
1. When guaranteed O(n log n) is required.
2. When extra memory should be minimal.
3. Good for large arrays with limited memory.
4. Useful when worst-case performance matters.
5. Heap concept is also useful for Priority Queues and Top-K problems.

#### 5. Trade-offs
1. Guaranteed O(n log n) performance.
2. In-place → O(1) extra space.
3. No O(n²) worst case like Quick Sort.
4. Not stable.
5. Usually slower than Quick Sort in practice.
6. More difficult to understand and implement than basic sorting algorithms.