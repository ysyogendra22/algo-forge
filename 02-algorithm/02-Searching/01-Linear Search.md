# Linear Search

#### 1. Definition — Must Know

Linear Search checks elements **one by one** until the target is found or the collection ends.

#### 2. Why It Is Used

1. Works on both **sorted and unsorted** data.
2. Simple when no ordering or special structure can help the search.
3. Useful for small datasets or one-time searches.

#### 3. How It Works

Example:

```text id="ls01"
Array  = [20, 40, 10, 30]
Target = 10
```

Search:

```text id="ls02"
20 → Not Match
40 → Not Match
10 → Found
```

Result:

```text id="ls03"
Index = 2
```

#### 4. Algorithm — Must Know

```text id="ls04"
1. Start from index 0.
2. Compare each element with target.
3. If equal → return index.
4. If array ends → return -1.
```

#### 5. Kotlin Implementation — Must Know

```kotlin id="ls05"
fun linearSearch(nums: IntArray, target: Int): Int {

    for (i in nums.indices) {
        if (nums[i] == target) {
            return i
        }
    }

    return -1
}
```

#### 6. Time & Space Complexity — Must Know

| Case | Time |
|---|---:|
| Best | `O(1)` |
| Average | `O(N)` |
| Worst | `O(N)` |
| Space | `O(1)` |

1. **Best:** Target is the first element.
2. **Worst:** Target is last or not present.
3. No extra data structure is required.

#### 7. Common Interview Uses

1. Find an element in an unsorted array.
2. Check whether a value exists.
3. Find first occurrence.
4. Find minimum / maximum by scanning.
5. Search when no faster searchable structure is available.

#### 8. Edge Cases / Common Mistakes

1. Empty array.
2. Single-element array.
3. Target not found.
4. Duplicate values — clarify whether to return first, last, or all occurrences.
5. Avoid unnecessary searching after the target is found.

#### 9. When to Use / When Not to Use

**Use when:**

1. Data is unsorted.
2. Dataset is small.
3. Only one/few searches are required.

**Avoid when:**

1. Large sorted data allows a faster search.
2. Many repeated lookups could benefit from a better data structure.

#### 10. Related Topics

1. Binary Search
2. HashMap / HashSet
3. Array Traversal

#### 11. Interview Must Remember

1. Linear Search checks elements **one by one**.
2. Works with **unsorted data**.
3. Best case → `O(1)`.
4. Average/Worst case → `O(N)`.
5. Space → `O(1)`.
6. Simple, but inefficient for repeated searches on large datasets.