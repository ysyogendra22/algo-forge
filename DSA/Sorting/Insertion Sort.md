#### 1. How it works

1. Treat the left part of the array as sorted.
2. Pick the next element.
3. Compare it with elements on the left.
4. Shift larger elements to the right.
5. Insert the element into its correct position.

#### 2. Complexity

1. Best: O(n) → Already sorted
2. Average: O(n²)
3. Worst: O(n²) → Reverse sorted
4. Space: O(1)

#### 3. Implementation - Kotlin

```
fun insertionSort(arr: IntArray) {
    for (i in 1 until arr.size) {
        val current = arr[i]
        var j = i - 1

        while (j >= 0 && arr[j] > current) {
            arr[j + 1] = arr[j]
            j--
        }

        arr[j + 1] = current
    }
}
```

#### 4. When to use

1. Small datasets.
2. Very good for nearly sorted data.
3. Useful when elements arrive one by one.
4. Often used inside hybrid sorting algorithms.
5. Avoid for large, randomly ordered datasets.

#### 5. Trade-offs

1. Simple to understand and implement.
2. In-place → O(1) extra space.
3. Stable sorting.
4. Fast for nearly sorted data → close to O(n).
5. Slow for large/reverse-sorted data → O(n²).
6. Generally more practical than Bubble Sort and Selection Sort.