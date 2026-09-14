# Advanced Binary Search on Answer

#### 1. Definition — Advanced

Advanced Binary Search on Answer applies Binary Search to a **large answer space** where:

1. The answer is not directly stored in the input.
2. A candidate answer can be checked.
3. The check produces a **monotonic** true/false pattern.

```text id="abs01"
F F F F T T T T
        ↑
   Minimum Valid
```

or:

```text id="abs02"
T T T T F F F
      ↑
  Maximum Valid
```

#### 2. Main Interview Pattern — Must Know

Most advanced problems can be reduced to:

```text id="abs03"
Find Answer Range
        ↓
Choose mid
        ↓
Check feasibility(mid)
        ↓
Eliminate half
```

The difficult part is usually **not Binary Search**.

It is designing:

```text id="abs04"
canDo(mid)
```

correctly.

#### 3. Minimum Valid Answer

Pattern:

```text id="abs05"
F F F T T T T
      ↑
```

If `mid` is valid:

```text id="abs06"
answer = mid
search LEFT
```

Otherwise:

```text id="abs07"
search RIGHT
```

Template:

```kotlin id="abs08"
fun findMinimum(leftValue: Long, rightValue: Long): Long {

    var left = leftValue
    var right = rightValue
    var answer = rightValue

    while (left <= right) {

        val mid = left + (right - left) / 2

        if (canDo(mid)) {
            answer = mid
            right = mid - 1
        } else {
            left = mid + 1
        }
    }

    return answer
}
```

#### 4. Maximum Valid Answer

Pattern:

```text id="abs09"
T T T T F F F
      ↑
```

If `mid` is valid:

```text id="abs10"
answer = mid
search RIGHT
```

Otherwise:

```text id="abs11"
search LEFT
```

Template:

```kotlin id="abs12"
fun findMaximum(leftValue: Long, rightValue: Long): Long {

    var left = leftValue
    var right = rightValue
    var answer = leftValue

    while (left <= right) {

        val mid = left + (right - left) / 2

        if (canDo(mid)) {
            answer = mid
            left = mid + 1
        } else {
            right = mid - 1
        }
    }

    return answer
}
```

#### 5. Important Advanced Pattern — Minimize the Maximum

Example:

```text id="abs13"
Split Array Largest Sum
```

Question:

> Split an array into `K` parts while minimizing the largest part sum.

Search range:

```text id="abs14"
left  = maximum element
right = sum of all elements
```

For each `mid`:

```text id="abs15"
Can we split the array into ≤ K parts
where every part sum ≤ mid?
```

If yes:

```text id="abs16"
mid is possible
→ try smaller
→ move LEFT
```

This is a very common FAANG pattern.

#### 6. Important Advanced Pattern — Maximize the Minimum

Example:

```text id="abs17"
Place K items while maximizing
the minimum distance between them.
```

Search over:

```text id="abs18"
minimum distance
```

For each `mid`:

```text id="abs19"
Can we place K items
with at least mid distance?
```

If yes:

```text id="abs20"
mid is possible
→ try larger
→ move RIGHT
```

Typical problems:

```text id="abs21"
Aggressive Cows
Magnetic Force Between Two Balls
```

#### 7. Common Search Range Patterns

**Capacity / Sum**

```text id="abs22"
left  = max element
right = total sum
```

**Speed**

```text id="abs23"
left  = 1
right = maximum required speed/value
```

**Distance**

```text id="abs24"
left  = 0 or 1
right = maxPosition - minPosition
```

**Time**

```text id="abs25"
left  = minimum possible time
right = safe maximum possible time
```

Choosing good bounds is part of the interview problem.

#### 8. Feasibility Function — Most Important

A feasibility check should answer only:

```text id="abs26"
Is candidate X possible?
```

Example:

```kotlin id="abs27"
fun canDo(limit: Long): Boolean {

    // Simulate using "limit"

    return true
}
```

Keep Binary Search and feasibility logic separate.

This makes the solution easier to reason about and debug.

#### 9. Common FAANG-Level Problems

1. Koko Eating Bananas.
2. Capacity to Ship Packages Within D Days.
3. Split Array Largest Sum.
4. Magnetic Force Between Two Balls.
5. Minimum Number of Days to Make Bouquets.
6. Allocate Books / workload partitioning.
7. Minimum Speed / Rate problems.
8. Minimum Time to Complete Tasks.

#### 10. Complexity

Suppose:

```text id="abs28"
Answer range = R
Feasibility check = O(N)
```

Then:

```text id="abs29"
Time  → O(N log R)
Space → usually O(1)
```

If sorting is required first:

```text id="abs30"
O(N log N + N log R)
```

#### 11. Use Long for Large Search Spaces — Must Know

Advanced problems often involve:

```text id="abs31"
sum
distance
capacity
time
multiplication
```

Prefer `Long` when values can become large.

```kotlin id="abs32"
var left = 0L
var right = 1_000_000_000_000L

val mid = left + (right - left) / 2
```

#### 12. Common Mistakes

1. Using Binary Search without proving monotonicity.
2. Searching the input instead of the **answer space**.
3. Incorrect minimum/maximum bounds.
4. Incorrect `canDo(mid)` logic.
5. Moving left/right in the wrong direction.
6. Confusing **minimum valid** with **maximum valid**.
7. Integer overflow.
8. Returning `mid` directly instead of preserving the best valid answer when needed.

#### 13. Interview Must Remember

1. Look for **minimize maximum** or **maximize minimum**.
2. Identify the **answer search space**.
3. Prove the feasibility result is **monotonic**.
4. Write a clean `canDo(mid)`.
5. Minimum valid → valid means **go left**.
6. Maximum valid → valid means **go right**.
7. Typical complexity → **`O(N log R)`**.
8. For large values, use **`Long`**.