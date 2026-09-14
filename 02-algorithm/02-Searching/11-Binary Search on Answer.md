# Binary Search on Answer

#### 1. Definition — Must Know

Binary Search on Answer means applying Binary Search to a **range of possible answers**, instead of searching directly inside an array.

Example:

```text id="bsa01"
Possible answers:

1  2  3  4  5  6  7  8  9  10
```

We use a condition to decide which half can be removed.

#### 2. When to Recognize It — Must Know

Look for questions like:

```text id="bsa02"
Minimum possible X
Maximum possible X
Smallest value that can...
Largest value that can...
Minimum capacity
Minimum speed
Maximum distance
```

Then ask:

```text id="bsa03"
Can I check whether a candidate answer is possible?
```

If yes, Binary Search on Answer may work.

#### 3. Core Requirement — Must Know

The condition must be **monotonic**.

Example:

```text id="bsa04"
Candidate:

1  2  3  4  5  6  7

Valid?

F  F  F  T  T  T  T
         ↑
    First Valid
```

Once the answer becomes valid, all larger values are also valid.

Or the opposite:

```text id="bsa05"
T  T  T  T  F  F  F
         ↑
     Last Valid
```

This monotonic behavior allows Binary Search.

#### 4. Core Pattern — Must Know

Most problems contain two parts:

```text id="bsa06"
Binary Search
      +
Feasibility Check
```

The feasibility function answers:

```text id="bsa07"
Can candidate X satisfy the requirement?
```

Usually:

```kotlin id="bsa08"
fun canDo(candidate: Int): Boolean
```

#### 5. Example — Minimum Eating Speed

Suppose:

```text id="bsa09"
Piles = [3, 6, 7, 11]
Hours = 8
```

Question:

```text id="bsa10"
What is the minimum eating speed
to finish everything within 8 hours?
```

Search space:

```text id="bsa11"
1 ... 11
```

For each speed:

```text id="bsa12"
Can all piles be finished within 8 hours?
```

The results become:

```text id="bsa13"
Invalid Invalid ... Valid Valid Valid
```

We need the:

```text id="bsa14"
First Valid Answer
```

#### 6. Generic Algorithm — Must Know

```text id="bsa15"
left  = minimum possible answer
right = maximum possible answer

while left <= right:

    mid = left + (right - left) / 2

    if mid is feasible:
        save mid
        search for better answer

    else:
        discard invalid half
```

For a **minimum valid answer**:

```text id="bsa16"
Valid   → move LEFT
Invalid → move RIGHT
```

#### 7. Kotlin Template — Minimum Valid Answer

```kotlin id="bsa17"
fun binarySearchAnswer(leftValue: Int, rightValue: Int): Int {

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

Where:

```kotlin id="bsa18"
fun canDo(value: Int): Boolean {
    // Check whether value satisfies the requirement
    return true
}
```

#### 8. Minimum vs Maximum Answer — Must Know

For **minimum valid**:

```text id="bsa19"
F F F T T T
      ↑

Valid → Search LEFT
```

For **maximum valid**:

```text id="bsa20"
T T T T F F
      ↑

Valid → Search RIGHT
```

This distinction is very important.

#### 9. Common Interview Patterns — Must Know

Binary Search on Answer commonly appears in:

1. Minimum capacity.
2. Minimum speed/rate.
3. Maximum minimum distance.
4. Minimum time.
5. Split / allocate array problems.
6. Minimum value satisfying a constraint.

Typical problems include:

```text id="bsa21"
Koko Eating Bananas
Capacity to Ship Packages
Allocate Books
Aggressive Cows / Maximum Distance
Split Array Largest Sum
```

#### 10. Choosing the Search Range — Must Know

You must correctly identify:

```text id="bsa22"
Minimum possible answer
Maximum possible answer
```

Example:

```text id="bsa23"
Minimum eating speed:

left  = 1
right = maximum pile
```

A wrong search range can produce incorrect results.

#### 11. Time & Space Complexity

If:

```text id="bsa24"
Search range = R
Feasibility check = O(N)
```

Then:

```text id="bsa25"
Time → O(N log R)
```

Because Binary Search performs:

```text id="bsa26"
O(log R)
```

feasibility checks.

Extra space is usually:

```text id="bsa27"
O(1)
```

depending on the feasibility function.

#### 12. Edge Cases / Common Mistakes

1. Applying Binary Search when the condition is not monotonic.
2. Choosing the wrong minimum/maximum search range.
3. Moving in the wrong direction after a valid answer.
4. Forgetting whether the problem asks for **minimum valid** or **maximum valid**.
5. Writing an incorrect feasibility function.
6. Integer overflow for large answer ranges.
7. Using `Int` when calculations may require `Long`.

#### 13. Interview Must Remember

1. Binary Search on Answer searches the **answer space**, not necessarily an array.
2. Look for **minimum/maximum value satisfying a condition**.
3. The feasibility condition must be **monotonic**.
4. Think: **Binary Search + `canDo(mid)`**.
5. Minimum valid → valid means search **left**.
6. Maximum valid → valid means search **right**.
7. Typical complexity → **`O(N log R)`** when each feasibility check is `O(N)`.