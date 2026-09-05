
#### 1. How it works
1. Find the maximum value in the array.
2. Create a count array for each possible value.
3. Count how many times each value appears.
4. Rebuild the array using those counts.
5. It does not compare elements directly.

#### 2. Complexity
1. Best: O(n + k)
2. Average: O(n + k)
3. Worst: O(n + k)
4. Space: O(k)
5. k = range of input values

#### 3. Implementation - Kotlin

```

fun countingSort(arr: IntArray) {
    if (arr.isEmpty()) return

    val max = arr.maxOrNull()!!
    val count = IntArray(max + 1)

    // Count occurrences
    for (num in arr) {
        count[num]++
    }

    // Rebuild sorted array
    var index = 0

    for (i in count.indices) {
        repeat(count[i]) {
            arr[index++] = i
        }
    }
}

```
#### 4. When to use
1. Data contains integers.
2. Range of values is small.
3. Good when many duplicate values exist.
4. Useful for things like ages, ratings, marks, or small ID ranges.
5. Avoid when the value range is very large.

#### 5. Trade-offs
1. Faster than O(n log n) sorting when the range is small.
2. No element-to-element comparisons are required.
3. Simple implementation for non-negative integers.
4. Requires O(k) extra memory.
5. Inefficient when the value range is very large.
6. Basic implementation above does not support negative numbers directly.
7. Basic implementation above is not stable; Counting Sort can be implemented as stable.