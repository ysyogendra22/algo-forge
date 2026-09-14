### Bubble Sort

#### How it works
- Compare two adjacent elements.
- If left > right → swap them.
- Repeat until sorted.
- After each round, the largest element moves to the end.

#### Complexity
- Best: O(n)
- Average: O(n²)
- Worst: O(n²)
- Space: O(1)

#### Implementation - Kotlin

```
fun bubbleSort(arr: IntArray) {
    for (i in 0 until arr.size - 1) {
        var swapped = false

        for (j in 0 until arr.size - i - 1) {
            if (arr[j] > arr[j + 1]) {
                val temp = arr[j]
                arr[j] = arr[j + 1]
                arr[j + 1] = temp
                swapped = true
            }
        }

        if (!swapped) break
    }
}

```

#### When to use
1.  Very small datasets.
2. Good for learning sorting basics.
3. Can work for already/nearly sorted data.
4. Avoid for large datasets.

#### Trade-offs
- Easy to understand and implement.
- In-place → O(1) extra space.
- Stable sorting.
- Slow for large data → O(n²).
- Usually worse than Quick Sort / Merge Sort.