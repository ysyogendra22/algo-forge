
#### 1. How it works

1. Sort numbers digit by digit.
2. Start from the least significant digit (ones place).
3. Then sort by tens, hundreds, and so on.
4. Use a stable sort like Counting Sort for each digit.
5. Repeat until all digits are processed.

#### 2. Complexity

1. Best: O(d × (n + k))
2. Average: O(d × (n + k))
3. Worst: O(d × (n + k))
4. Space: O(n + k)
5. d = number of digits
6. k = digit range, usually 10

#### 3. Implementation - Kotlin

```
fun radixSort(arr: IntArray) {
    if (arr.isEmpty()) return

    val max = arr.maxOrNull()!!
    var exp = 1

    while (max / exp > 0) {
        countingSortByDigit(arr, exp)

        if (exp > max / 10) break
        exp *= 10
    }
}

fun countingSortByDigit(arr: IntArray, exp: Int) {
    val output = IntArray(arr.size)
    val count = IntArray(10)

    for (num in arr) {
        val digit = (num / exp) % 10
        count[digit]++
    }

    for (i in 1 until 10) {
        count[i] += count[i - 1]
    }

    for (i in arr.lastIndex downTo 0) {
        val digit = (arr[i] / exp) % 10
        output[count[digit] - 1] = arr[i]
        count[digit]--
    }

    for (i in arr.indices) {
        arr[i] = output[i]
    }
}

```

#### 4. When to use

1. Large number of integers.
2. Good when numbers have a limited number of digits.
3. Useful for fixed-length numeric keys.
4. Can be faster than comparison-based sorting in suitable cases.
5. Avoid when values have very large or highly variable key lengths.

#### 5. Trade-offs

1. Can be faster than O(n log n) comparison sorting.
2. Does not compare elements directly.
3. Stable when the sorting used for each digit is stable.
4. Requires extra memory.
5. More complex than basic sorting algorithms.
6. Performance depends on the number of digits.
7. This implementation supports non-negative integers only.