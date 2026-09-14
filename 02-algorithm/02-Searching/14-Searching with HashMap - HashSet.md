# Searching with HashMap / HashSet

#### 1. Definition — Good to Know

HashMap and HashSet provide **fast lookup** using hashing.

Typical lookup:

```text
Average → O(1)
```

Use them when you need to quickly check whether a value or key has already been seen.

#### 2. HashSet vs HashMap

**HashSet**

Store only values:

```text
{10, 20, 30}
```

Use when you only need:

```text
Does this value exist?
```

**HashMap**

Store key-value pairs:

```text
10 → 0
20 → 1
30 → 2
```

Use when you need:

```text
Does this key exist?
+
Associated information
```

#### 3. HashSet Search — Must Know

```kotlin
val seen = HashSet<Int>()

seen.add(10)
seen.add(20)

if (seen.contains(10)) {
    println("Found")
}
```

Typical operations:

```text
add()      → O(1) average
contains() → O(1) average
remove()   → O(1) average
```

#### 4. HashMap Search — Must Know

```kotlin
val map = HashMap<Int, Int>()

map[10] = 0
map[20] = 1

if (map.containsKey(10)) {
    println(map[10])
}
```

Typical operations:

```text
put       → O(1) average
get       → O(1) average
contains  → O(1) average
remove    → O(1) average
```

#### 5. Common Pattern — Seen / Duplicate

```kotlin
fun containsDuplicate(nums: IntArray): Boolean {

    val seen = HashSet<Int>()

    for (num in nums) {

        if (num in seen) {
            return true
        }

        seen.add(num)
    }

    return false
}
```

Pattern:

```text
Visit element
    ↓
Already in Set?
    ↓
Yes → Duplicate
No  → Add to Set
```

#### 6. Common Pattern — Complement Lookup

Example: **Two Sum**

```text
target = 9
current = 7

needed = 9 - 7 = 2
```

Check whether `2` was already seen.

```kotlin
fun twoSum(nums: IntArray, target: Int): IntArray {

    val map = HashMap<Int, Int>()

    for (i in nums.indices) {

        val needed = target - nums[i]

        if (map.containsKey(needed)) {
            return intArrayOf(map[needed]!!, i)
        }

        map[nums[i]] = i
    }

    return intArrayOf()
}
```

#### 7. Time & Space Complexity — Must Know

For processing `N` elements:

```text
Time  → O(N) average
Space → O(N)
```

Each HashMap / HashSet lookup is typically:

```text
O(1) average
```

Hash-based operations can degrade in pathological collision cases, but `O(1)` average is the standard interview expectation.

#### 8. When to Use

Think HashMap / HashSet when you see:

1. **Have I seen this before?**
2. **Does this value exist?**
3. **Find duplicates.**
4. **Find a complement.**
5. **Need value → index/count mapping.**
6. **Need repeated fast lookups.**

#### 9. HashSet vs HashMap — Decision

```text
Only need existence?
        ↓
     HashSet


Need additional information?
(index, count, mapping)
        ↓
     HashMap
```

#### 10. Common Mistakes

1. Using HashMap when only existence is needed.
2. Forgetting HashMap/HashSet uses extra `O(N)` space.
3. Assuming elements are returned in sorted order.
4. In Two Sum, inserting before checking can accidentally reuse the same element in some implementations.
5. Assuming hashing is always worst-case `O(1)`.

#### 11. Interview Must Remember

1. HashMap / HashSet → **`O(1)` average lookup**.
2. HashSet → **value/existence**.
3. HashMap → **key + associated data**.
4. Common patterns → **seen, duplicate, complement, mapping**.
5. Processing an array with hashing is commonly **`O(N)` time + `O(N)` space**.