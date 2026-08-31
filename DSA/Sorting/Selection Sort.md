
#### How it works
1.  Find the smallest element.
2. Swap it with the first unsorted element.
3. Repeat for the remaining array.
4. After each round, one element reaches its correct position.

#### Complexity
1. Best: O(n²)
2. Average: O(n²)
3. Worst: O(n²)
4. Space: O(1)

####  Implementation - Kotlin

```

fun selectionSort(arr: IntArray) {
    for (i in 0 until arr.size - 1) {
        var minIndex = i

        for (j in i + 1 until arr.size) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j
            }
        }

        if (minIndex != i) {
            val temp = arr[i]
            arr[i] = arr[minIndex]
            arr[minIndex] = temp
        }
    }
}

```

#### When to use
1.  Very small datasets.
2. When minimizing number of swaps is useful.
3. Good for learning sorting basics.
4. Avoid for large datasets.

####  Trade-offs
1. Easy to understand and implement.
2. In-place → O(1) extra space.
3. Performs fewer swaps than Bubble Sort.
4. Usually not stable.
5. Still O(n²) even if already sorted.
6. Usually worse than Quick Sort / Merge Sort for large data.