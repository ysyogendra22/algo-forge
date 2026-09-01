
#### 1. How it works

1. Create multiple buckets.
2. Distribute elements into buckets based on their values.
3. Sort each bucket separately.
4. Combine all buckets in order.
5. Works best when data is evenly distributed.

#### 2. Complexity

1. Best: O(n + k)
2. Average: O(n + k)
3. Worst: O(n²)
4. Space: O(n + k)
5. k = number of buckets

#### 3. Implementation - Kotlin
```

fun bucketSort(arr: IntArray) {
    if (arr.isEmpty()) return

    val min = arr.minOrNull()!!
    val max = arr.maxOrNull()!!
    val bucketCount = arr.size

    if (min == max) return

    val buckets = Array(bucketCount) { mutableListOf<Int>() }

    // Put elements into buckets
    for (num in arr) {
        val index = ((num.toLong() - min) * (bucketCount - 1) /
                (max.toLong() - min)).toInt()

        buckets[index].add(num)
    }

    // Sort each bucket and combine
    var index = 0

    for (bucket in buckets) {
        bucket.sort()

        for (num in bucket) {
            arr[index++] = num
        }
    }
}

```

#### 4. When to use

1. Data is uniformly/evenly distributed.
2. Useful when values can be divided into ranges.
3. Good for large datasets with a known distribution.
4. Common example is sorting floating-point values between 0 and 1.
5. Avoid when data is heavily concentrated in a few buckets.

#### 5. Trade-offs

1. Average performance can be close to O(n).
2. Can outperform comparison sorts when data is well distributed.
3. Requires extra memory for buckets.
4. Performance depends heavily on bucket distribution.
5. Poor bucket distribution can lead to O(n²).
6. Requires another sorting method to sort elements inside each bucket.