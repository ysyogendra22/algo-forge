# First & Last Occurrence

#### 1. Definition — Must Know

Find the **first and last index** of a target in a sorted array containing duplicates.

Example:

```text
Array  = [1, 2, 2, 2, 3, 4]
Target = 2

First = 1
Last  = 3
```

#### 2. Why It Is Used

Normal Binary Search may return **any occurrence**.

For duplicates, we may need:

1. First occurrence.
2. Last occurrence.
3. Range of the target.
4. Number of occurrences.

#### 3. Core Idea — Must Know

When the target is found, **don't stop searching**.

For first occurrence:

```text
Found target
    ↓
Save index
    ↓
Continue LEFT
```

For last occurrence:

```text
Found target
    ↓
Save index
    ↓
Continue RIGHT
```

#### 4. First Occurrence — Algorithm

When:

```text
nums[mid] == target
```

Save the result and continue left:

```text
result = mid
right = mid - 1
```

#### 5. Kotlin — First Occurrence

```kotlin
fun firstOccurrence(nums: IntArray, target: Int): Int {

    var left = 0
    var right = nums.lastIndex
    var result = -1

    while (left <= right) {

        val mid = left + (right - left) / 2

        when {
            nums[mid] == target -> {
                result = mid
                right = mid - 1
            }

            nums[mid] < target -> left = mid + 1

            else -> right = mid - 1
        }
    }

    return result
}
```

#### 6. Last Occurrence — Algorithm

When:

```text
nums[mid] == target
```

Save the result and continue right:

```text
result = mid
left = mid + 1
```

#### 7. Kotlin — Last Occurrence

```kotlin
fun lastOccurrence(nums: IntArray, target: Int): Int {

    var left = 0
    var right = nums.lastIndex
    var result = -1

    while (left <= right) {

        val mid = left + (right - left) / 2

        when {
            nums[mid] == target -> {
                result = mid
                left = mid + 1
            }

            nums[mid] < target -> left = mid + 1

            else -> right = mid - 1
        }
    }

    return result
}
```

#### 8. Find Both

```kotlin
fun searchRange(nums: IntArray, target: Int): IntArray {
    return intArrayOf(
        firstOccurrence(nums, target),
        lastOccurrence(nums, target)
    )
}
```

Example:

```text
[1, 2, 2, 2, 3]

Target = 2

Result = [1, 3]
```

#### 9. Count Occurrences — Good to Know

If target exists:

```text
count = last - first + 1
```

Example:

```text
first = 1
last  = 3

count = 3 - 1 + 1
      = 3
```

#### 10. Time & Space Complexity — Must Know

Two Binary Searches are performed.

```text
Time  → O(log N)
Space → O(1)
```

It is still `O(log N)` because:

```text
O(log N) + O(log N) = O(log N)
```

#### 11. Edge Cases / Common Mistakes

1. Target not present → return `-1`.
2. Only one occurrence → first and last are the same.
3. All elements are the target.
4. Target at beginning or end.
5. Returning immediately when target is found.
6. Mixing up left/right movement after finding the target.

#### 12. Interview Must Remember

1. Array should be **sorted**.
2. Normal Binary Search may return any duplicate.
3. First occurrence → **find target, then move left**.
4. Last occurrence → **find target, then move right**.
5. Save `mid` before continuing the search.
6. Time → `O(log N)`, Space → `O(1)`.