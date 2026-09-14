# Peak Element

#### 1. Definition — Must Know

A **peak element** is greater than its neighboring elements.

```text id="peak01"
nums[i] > nums[i - 1]
and
nums[i] > nums[i + 1]
```

Example:

```text id="peak02"
[1, 3, 5, 4, 2]
       ↑
      Peak
```

`5` is a peak.

#### 2. Important Point — Must Know

The array does **not need to be sorted**.

There may also be **multiple peaks**.

```text id="peak03"
[1, 4, 2, 5, 3]
    ↑     ↑
```

Usually, returning **any peak index** is enough.

#### 3. Core Idea — Must Know

Compare:

```text id="peak04"
nums[mid]
```

with:

```text id="peak05"
nums[mid + 1]
```

If:

```text id="peak06"
nums[mid] < nums[mid + 1]
```

we are moving upward:

```text id="peak07"
       /
      /
mid  →  mid+1

Peak exists on RIGHT
```

So:

```text id="peak08"
left = mid + 1
```

Otherwise:

```text id="peak09"
nums[mid] > nums[mid + 1]
```

we are moving downward:

```text id="peak10"
Peak exists at mid or on LEFT
```

So:

```text id="peak11"
right = mid
```

#### 4. Algorithm — Must Know

```text id="peak12"
left = 0
right = n - 1

while left < right:

    mid = left + (right - left) / 2

    if nums[mid] < nums[mid + 1]:
        left = mid + 1

    else:
        right = mid

return left
```

#### 5. Kotlin Implementation — Must Know

```kotlin id="peak13"
fun findPeakElement(nums: IntArray): Int {

    var left = 0
    var right = nums.lastIndex

    while (left < right) {

        val mid = left + (right - left) / 2

        if (nums[mid] < nums[mid + 1]) {
            left = mid + 1
        } else {
            right = mid
        }
    }

    return left
}
```

#### 6. Example

```text id="peak14"
nums = [1, 2, 3, 5, 4, 2]
```

At some point:

```text id="peak15"
3 < 5

Move RIGHT
```

Then:

```text id="peak16"
5 > 4

Keep LEFT side including 5
```

Eventually:

```text id="peak17"
left == right

Peak Index = 3
Peak Value = 5
```

#### 7. Why Binary Search Works

We don't need a fully sorted array.

We only need to know the **slope direction**:

```text id="peak18"
nums[mid] < nums[mid + 1]
        ↓
Go Right


nums[mid] > nums[mid + 1]
        ↓
Go Left / Keep Mid
```

This lets us eliminate half of the search space.

#### 8. Time & Space Complexity — Must Know

```text id="peak19"
Time  → O(log N)
Space → O(1)
```

A linear scan could find a peak in:

```text id="peak20"
O(N)
```

but Binary Search gives `O(log N)`.

#### 9. Edge Cases / Common Mistakes

1. Single element → it is a peak.
2. Peak can be at index `0`.
3. Peak can be at the last index.
4. Multiple peaks → any valid peak may be returned.
5. Don't access `nums[mid - 1]` unnecessarily.
6. `mid + 1` is safe because the loop uses `left < right`.
7. Don't assume the entire array is sorted.

#### 10. Related Topics

1. Binary Search
2. Binary Search on Answer
3. Find Minimum in Rotated Sorted Array

#### 11. Interview Must Remember

1. Peak → element greater than its neighbors.
2. Array does **not** need to be sorted.
3. Multiple peaks may exist.
4. Compare `nums[mid]` with `nums[mid + 1]`.
5. Rising slope → move **right**.
6. Falling slope → keep `mid` and move **left**.
7. Time → **`O(log N)`**.