# Lower Bound / Upper Bound

#### 1. Definition — Must Know

For a **sorted array**:

1. **Lower Bound** → first index where value is **`>= target`**.
2. **Upper Bound** → first index where value is **`> target`**.

Example:

```text
Array  = [1, 2, 2, 2, 4, 6]
Target = 2

Lower Bound = 1
Upper Bound = 4
```

#### 2. Why It Is Used

Useful when we need:

1. First valid position for a target.
2. Insertion position while keeping the array sorted.
3. Range of duplicate values.
4. Number of occurrences of a target.

#### 3. Core Difference — Must Know

```text
Lower Bound → first value >= target

Upper Bound → first value > target
```

This is the main rule to remember.

#### 4. Lower Bound — How It Works

Example:

```text
Array  = [1, 3, 3, 5, 7]
Target = 3

        ↓
[1, 3, 3, 5, 7]

Lower Bound = 1
```

When:

```text
nums[mid] >= target
```

`mid` can be the answer, but there may be an earlier valid position.

So:

```text
answer = mid
right = mid - 1
```

Otherwise:

```text
left = mid + 1
```

#### 5. Lower Bound — Kotlin

```kotlin
fun lowerBound(nums: IntArray, target: Int): Int {

    var left = 0
    var right = nums.lastIndex
    var answer = nums.size

    while (left <= right) {

        val mid = left + (right - left) / 2

        if (nums[mid] >= target) {
            answer = mid
            right = mid - 1
        } else {
            left = mid + 1
        }
    }

    return answer
}
```

If no valid element exists:

```text
return nums.size
```

#### 6. Upper Bound — How It Works

Example:

```text
Array  = [1, 3, 3, 5, 7]
Target = 3

              ↓
[1, 3, 3, 5, 7]

Upper Bound = 3
```

When:

```text
nums[mid] > target
```

`mid` can be the answer, so continue searching left.

```text
answer = mid
right = mid - 1
```

Otherwise:

```text
left = mid + 1
```

#### 7. Upper Bound — Kotlin

```kotlin
fun upperBound(nums: IntArray, target: Int): Int {

    var left = 0
    var right = nums.lastIndex
    var answer = nums.size

    while (left <= right) {

        val mid = left + (right - left) / 2

        if (nums[mid] > target) {
            answer = mid
            right = mid - 1
        } else {
            left = mid + 1
        }
    }

    return answer
}
```

#### 8. Lower vs Upper Bound — Must Know

| | Lower Bound | Upper Bound |
|---|---|---|
| Finds | First `>= target` | First `> target` |
| Can point to target | Yes | No |
| Useful for insertion | Yes | Yes |
| Handles duplicates | Yes | Yes |

Easy memory:

```text
Lower → >=
Upper → >
```

#### 9. Count Target Occurrences — Good to Know

For a sorted array:

```text
count = upperBound - lowerBound
```

Example:

```text
[1, 2, 2, 2, 4]

lowerBound(2) = 1
upperBound(2) = 4

count = 4 - 1
      = 3
```

#### 10. Important Difference from First / Last Occurrence

First occurrence:

```text
First index where value == target
```

Lower Bound:

```text
First index where value >= target
```

So if target doesn't exist:

```text
Array  = [1, 3, 5, 7]
Target = 4

Lower Bound = 2
              ↑
              5
```

Lower Bound can still return a valid insertion position.

#### 11. Time & Space Complexity — Must Know

```text
Time  → O(log N)
Space → O(1)
```

Both use Binary Search.

#### 12. Edge Cases / Common Mistakes

1. Empty array → returns `0`.
2. Target smaller than all elements → returns `0`.
3. Target larger than all elements → returns `N`.
4. Duplicate values.
5. Confusing `>=` with `>`.
6. Assuming the returned index always contains the target.

#### 13. Interview Must Remember

1. Array must be **sorted**.
2. Lower Bound → first **`>= target`**.
3. Upper Bound → first **`> target`**.
4. If no valid position exists → return `N`.
5. `upperBound - lowerBound` can count duplicates.
6. Both run in **`O(log N)`**.