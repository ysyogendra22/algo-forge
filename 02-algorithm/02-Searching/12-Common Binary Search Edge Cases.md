# Common Binary Search Edge Cases

#### 1. Empty Array — Must Know

```text
[]
```

1. No element can be found.
2. Return the expected not-found result, usually `-1`.

#### 2. Single Element — Must Know

```text
[5]
```

Test both:

```text
Target = 5 → Found
Target = 3 → Not Found
```

#### 3. Target at Boundaries — Must Know

Always consider:

```text
[1, 3, 5, 7, 9]
 ↑           ↑
First       Last
```

Binary Search must correctly find both boundary elements.

#### 4. Target Not Present — Must Know

```text
Array  = [1, 3, 5, 7]
Target = 4
```

The loop must terminate correctly without an infinite loop.

#### 5. Duplicate Elements — Must Know

```text
[1, 2, 2, 2, 3]
```

Normal Binary Search can return **any occurrence**.

If the question asks for:

```text
First occurrence
Last occurrence
Lower bound
Upper bound
```

use the appropriate Binary Search variant.

#### 6. Two Elements — Must Know

Small arrays often expose boundary bugs.

```text
[2, 5]
```

Test:

```text
Target = 2
Target = 5
Target = 3
```

#### 7. Correct Loop Condition — Must Know

For the standard closed interval:

```kotlin
var left = 0
var right = nums.lastIndex
```

use:

```kotlin
while (left <= right)
```

If using a different interval convention, the loop condition and updates must match it.

#### 8. Correct Boundary Updates — Must Know

Standard Binary Search:

```kotlin
if (nums[mid] < target) {
    left = mid + 1
} else {
    right = mid - 1
}
```

A common mistake is:

```text
left = mid
right = mid
```

when `mid` has already been checked.

This can cause an **infinite loop**.

#### 9. Mid Calculation — Must Know

Prefer:

```kotlin
val mid = left + (right - left) / 2
```

Instead of:

```kotlin
val mid = (left + right) / 2
```

The first form avoids potential integer overflow.

#### 10. Search Range Boundary — Must Know

Some problems allow the answer to be:

```text
0 ... N
```

Example:

```text
Search Insert Position
Lower Bound
Upper Bound
```

So don't automatically assume every Binary Search range is:

```text
0 ... N - 1
```

#### 11. Integer Overflow — Good to Know

For large values, especially **Binary Search on Answer**, use `Long` when needed.

```kotlin
val mid = left + (right - left) / 2
```

This is common in problems involving:

```text
Capacity
Distance
Time
Sum
Speed
```

#### 12. Quick Interview Checklist

Before submitting Binary Search, check:

```text
1. Empty input?

2. One / two elements?

3. Target at first / last?

4. Target missing?

5. Duplicates?

6. Correct left/right boundaries?

7. Correct < vs <=?

8. Can the loop get stuck?

9. Can calculations overflow?
```

#### 13. Interview Must Remember

1. Most Binary Search bugs are **boundary bugs**.
2. Be consistent with your interval: `[left, right]` or `[left, right)`.
3. Test **0, 1, and 2-element inputs** mentally.
4. Handle duplicates according to what the question asks.
5. Make sure every iteration **reduces the search space**.
6. Use `Long` when the search space or calculations can overflow `Int`.