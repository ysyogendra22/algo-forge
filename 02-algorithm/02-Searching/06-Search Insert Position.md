# Search Insert Position

#### 1. Definition — Must Know

Given a **sorted array**, find:

1. The index of the target if it exists.
2. Otherwise, the index where it should be inserted to keep the array sorted.

Example:

```text id="sip01"
Array  = [1, 3, 5, 6]
Target = 5

Result = 2
```

If target does not exist:

```text id="sip02"
Array  = [1, 3, 5, 6]
Target = 2

Result = 1
```

Because:

```text id="sip03"
[1, 2, 3, 5, 6]
    ↑
```

#### 2. Core Idea — Must Know

Search Insert Position is essentially:

```text id="sip04"
Lower Bound
```

We need the first index where:

```text id="sip05"
nums[index] >= target
```

If no such element exists:

```text id="sip06"
Answer = nums.size
```

#### 3. How It Works

Example:

```text id="sip07"
Array  = [1, 3, 5, 6]
Target = 2
```

Binary Search:

```text id="sip08"
mid = 1
nums[mid] = 3

3 >= 2

Possible answer = 1
Search left for an earlier position
```

No earlier valid position exists.

```text id="sip09"
Result = 1
```

#### 4. Algorithm — Must Know

```text id="sip10"
1. left = 0
2. right = n - 1
3. answer = n

4. If nums[mid] >= target:
      answer = mid
      search LEFT

5. Otherwise:
      search RIGHT
```

#### 5. Kotlin Implementation — Must Know

```kotlin id="sip11"
fun searchInsert(nums: IntArray, target: Int): Int {

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

#### 6. Simpler Binary Search Version

Another common implementation:

```kotlin id="sip12"
fun searchInsert(nums: IntArray, target: Int): Int {

    var left = 0
    var right = nums.size

    while (left < right) {

        val mid = left + (right - left) / 2

        if (nums[mid] < target) {
            left = mid + 1
        } else {
            right = mid
        }
    }

    return left
}
```

At the end:

```text id="sip13"
left = insertion position
```

#### 7. Time & Space Complexity — Must Know

```text id="sip14"
Time  → O(log N)
Space → O(1)
```

#### 8. Important Edge Cases

```text id="sip15"
Array = [1, 3, 5, 6]
```

Target already exists:

```text id="sip16"
Target = 5 → 2
```

Insert at beginning:

```text id="sip17"
Target = 0 → 0
```

Insert in middle:

```text id="sip18"
Target = 2 → 1
```

Insert at end:

```text id="sip19"
Target = 7 → 4
```

#### 9. Common Mistakes

1. Using Linear Search instead of Binary Search.
2. Forgetting insertion can happen at index `N`.
3. Returning `-1` when the target doesn't exist.
4. Incorrect boundary handling.
5. Not recognizing this as a **Lower Bound** problem.

#### 10. Related Topics

1. Binary Search
2. Lower Bound
3. First Occurrence

#### 11. Interview Must Remember

1. Input is **sorted**.
2. Target exists → return its position.
3. Target doesn't exist → return insertion position.
4. Equivalent to finding the first index where **`nums[i] >= target`**.
5. This is a **Lower Bound pattern**.
6. Time → `O(log N)`, Space → `O(1)`.