# Binary Search on Rotated Sorted Array

#### 1. Definition — Must Know

A rotated sorted array is a sorted array rotated around some pivot.

```text id="rsa01"
Sorted:
[1, 2, 3, 4, 5, 6, 7]

Rotated:
[4, 5, 6, 7, 1, 2, 3]
```

Goal: find a target in **`O(log N)`**.

#### 2. Core Idea — Must Know

After rotation, the entire array is not sorted.

But at every Binary Search step:

```text id="rsa02"
At least one half is sorted.
```

So:

```text id="rsa03"
1. Find mid.
2. Identify the sorted half.
3. Check if target lies inside that half.
4. Keep that half or discard it.
```

#### 3. How to Identify the Sorted Half

If:

```text id="rsa04"
nums[left] <= nums[mid]
```

then:

```text id="rsa05"
LEFT half is sorted.
```

Otherwise:

```text id="rsa06"
RIGHT half is sorted.
```

#### 4. Case 1 — Left Half Is Sorted

Example:

```text id="rsa07"
[4, 5, 6, 7, 1, 2, 3]
 L        M
```

Left side:

```text id="rsa08"
[4, 5, 6, 7]
```

is sorted.

Check whether:

```text id="rsa09"
nums[left] <= target < nums[mid]
```

If yes:

```text id="rsa10"
Search LEFT
```

Otherwise:

```text id="rsa11"
Search RIGHT
```

#### 5. Case 2 — Right Half Is Sorted

If the left half is not sorted, the right half must be sorted.

Check:

```text id="rsa12"
nums[mid] < target <= nums[right]
```

If yes:

```text id="rsa13"
Search RIGHT
```

Otherwise:

```text id="rsa14"
Search LEFT
```

#### 6. Kotlin Implementation — Must Know

Assume all values are **unique**.

```kotlin id="rsa15"
fun search(nums: IntArray, target: Int): Int {

    var left = 0
    var right = nums.lastIndex

    while (left <= right) {

        val mid = left + (right - left) / 2

        if (nums[mid] == target) {
            return mid
        }

        // Left half is sorted
        if (nums[left] <= nums[mid]) {

            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1
            } else {
                left = mid + 1
            }

        } else {

            // Right half is sorted
            if (nums[mid] < target && target <= nums[right]) {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
    }

    return -1
}
```

#### 7. Example

```text id="rsa16"
nums   = [4, 5, 6, 7, 0, 1, 2]
target = 0
```

First:

```text id="rsa17"
mid = 3
nums[mid] = 7

Left half [4,5,6,7] is sorted.

0 is not inside [4,7).

Discard LEFT.
```

Now:

```text id="rsa18"
[0, 1, 2]
```

Continue Binary Search until:

```text id="rsa19"
0 → Found at index 4
```

#### 8. Time & Space Complexity — Must Know

```text id="rsa20"
Time  → O(log N)
Space → O(1)
```

We still discard approximately half of the search space each iteration.

#### 9. Duplicates — Good to Know

The standard solution usually assumes:

```text id="rsa21"
All elements are unique.
```

With duplicates:

```text id="rsa22"
[1, 0, 1, 1, 1]
```

it may become impossible to determine which half is sorted immediately.

A common approach is to shrink equal boundaries.

Worst case can degrade to:

```text id="rsa23"
O(N)
```

Study the duplicate variant separately if needed.

#### 10. Edge Cases / Common Mistakes

1. Empty array.
2. Single element.
3. Array not rotated.
4. Target does not exist.
5. Target at pivot.
6. Mixing `<` and `<=` in range checks.
7. Incorrectly identifying the sorted half.
8. Forgetting that the unique-elements solution needs adjustment for duplicates.

#### 11. Interview Must Remember

1. Rotated array is still **partially sorted**.
2. At least one half is sorted at every step.
3. `nums[left] <= nums[mid]` → left half sorted.
4. Otherwise → right half sorted.
5. Check whether target belongs to the sorted half.
6. Discard the other half.
7. Time → **`O(log N)`** for unique elements.