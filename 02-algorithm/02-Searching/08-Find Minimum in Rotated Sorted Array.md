# Find Minimum in Rotated Sorted Array

#### 1. Definition — Must Know

Find the **smallest element** in a rotated sorted array.

Example:

```text id="fmr01"
Original:
[1, 2, 3, 4, 5]

Rotated:
[4, 5, 1, 2, 3]

Minimum = 1
```

Goal:

```text id="fmr02"
O(log N)
```

#### 2. Core Idea — Must Know

The minimum is the point where the rotated array changes from:

```text id="fmr03"
Large values → Small values
```

Example:

```text id="fmr04"
[4, 5, 6, 7, 1, 2, 3]
             ↑
          Minimum
```

Use Binary Search to find this point.

#### 3. Key Comparison — Must Know

Compare:

```text id="fmr05"
nums[mid]
```

with:

```text id="fmr06"
nums[right]
```

If:

```text id="fmr07"
nums[mid] > nums[right]
```

the minimum must be on the **right side**:

```text id="fmr08"
left = mid + 1
```

Otherwise:

```text id="fmr09"
nums[mid] <= nums[right]
```

the minimum is at `mid` or on the **left side**:

```text id="fmr10"
right = mid
```

#### 4. Why `right = mid`?

Because `mid` itself could be the minimum.

Example:

```text id="fmr11"
[5, 1, 2, 3, 4]
    ↑
   mid
```

Removing `mid` could remove the correct answer.

So use:

```text id="fmr12"
right = mid
```

not:

```text id="fmr13"
right = mid - 1
```

#### 5. Algorithm — Must Know

```text id="fmr14"
left = 0
right = n - 1

while left < right:

    mid = left + (right - left) / 2

    if nums[mid] > nums[right]:
        left = mid + 1

    else:
        right = mid

return nums[left]
```

#### 6. Kotlin Implementation — Must Know

Assume the array contains **unique elements**.

```kotlin id="fmr15"
fun findMin(nums: IntArray): Int {

    var left = 0
    var right = nums.lastIndex

    while (left < right) {

        val mid = left + (right - left) / 2

        if (nums[mid] > nums[right]) {
            left = mid + 1
        } else {
            right = mid
        }
    }

    return nums[left]
}
```

#### 7. Example

```text id="fmr16"
nums = [4, 5, 6, 7, 0, 1, 2]
```

First:

```text id="fmr17"
mid = 3
nums[mid] = 7
nums[right] = 2

7 > 2

Minimum is on RIGHT.
```

Search:

```text id="fmr18"
[0, 1, 2]
```

Eventually:

```text id="fmr19"
left == right

nums[left] = 0
```

#### 8. Not Rotated Case

Example:

```text id="fmr20"
[1, 2, 3, 4, 5]
```

The same algorithm works.

Result:

```text id="fmr21"
1
```

No separate logic is required.

#### 9. Time & Space Complexity — Must Know

```text id="fmr22"
Time  → O(log N)
Space → O(1)
```

Each step removes roughly half of the remaining search space.

#### 10. Duplicates — Good to Know

With duplicates:

```text id="fmr23"
[2, 2, 2, 0, 1, 2]
```

If:

```text id="fmr24"
nums[mid] == nums[right]
```

we may not know which side contains the minimum.

A common approach is:

```text id="fmr25"
right--
```

Worst-case complexity can become:

```text id="fmr26"
O(N)
```

#### 11. Edge Cases / Common Mistakes

1. Single element.
2. Array not rotated.
3. Minimum at index `0`.
4. Minimum near the end.
5. Using `left <= right` unnecessarily for this pattern.
6. Using `right = mid - 1` and accidentally removing the minimum.
7. Not handling duplicates when the problem allows them.

#### 12. Interview Must Remember

1. Compare **`nums[mid]` with `nums[right]`**.
2. `nums[mid] > nums[right]` → minimum is **right of mid**.
3. Otherwise → minimum is **at mid or left of mid**.
4. Use `left = mid + 1` or `right = mid`.
5. Stop when `left == right`.
6. `nums[left]` is the minimum.
7. Time → **`O(log N)`** for unique elements.