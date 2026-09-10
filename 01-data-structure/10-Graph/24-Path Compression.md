# Path Compression

#### 1. Definition — Must Know

1. **Path Compression** is an optimization used in **Union-Find / DSU**.
2. It makes every visited node point closer/directly to the **root** during `find()`.
3. This makes future `find()` operations much faster.

#### 2. Why It Is Needed — Must Know

Without optimization, DSU can become a long chain:

```text id="pc01"
4 → 3 → 2 → 1 → 0
```

Finding the root of `4` requires:

```text id="pc02"
4 → 3 → 2 → 1 → 0
```

Multiple steps are required.

Path Compression reduces this depth.

#### 3. How It Works — Must Know

Call:

```text id="pc03"
find(4)
```

Before:

```text id="pc04"
4 → 3 → 2 → 1 → 0
```

Root:

```text id="pc05"
0
```

During `find()`, update each visited node to point directly to the root.

After:

```text id="pc06"
    0
  / | | \
 1  2 3  4
```

Now:

```text id="pc07"
4 → 0
3 → 0
2 → 0
1 → 0
```

Future `find()` calls become much faster.

#### 4. Core Logic — Must Know

Normal Find:

```kotlin id="pc08"
fun find(x: Int): Int {

    if (parent[x] == x) {
        return x
    }

    return find(parent[x])
}
```

With Path Compression:

```kotlin id="pc09"
fun find(x: Int): Int {

    if (parent[x] != x) {
        parent[x] = find(parent[x])
    }

    return parent[x]
}
```

The most important line:

```kotlin id="pc10"
parent[x] = find(parent[x])
```

#### 5. What This Line Does — Must Know

```kotlin id="pc11"
parent[x] = find(parent[x])
```

Two things happen:

```text id="pc12"
find(parent[x])
        ↓
Find actual root

parent[x] = root
        ↓
Connect x directly to root
```

Example:

```text id="pc13"
parent[4] = find(parent[4])

parent[4] = find(3)

parent[4] = 0
```

#### 6. Before vs After

Before:

```text id="pc14"
4
↓
3
↓
2
↓
1
↓
0
```

After `find(4)`:

```text id="pc15"
    0
  / | | \
 1  2 3  4
```

The DSU becomes much flatter.

#### 7. Complexity — Must Know

Without optimizations, worst-case `find()` can approach:

```text id="pc16"
O(N)
```

With:

```text id="pc17"
Path Compression
+
Union by Rank / Size
```

amortized complexity becomes:

```text id="pc18"
O(α(N))
```

Practically:

```text id="pc19"
≈ O(1)
```

`α(N)` is the inverse Ackermann function and grows extremely slowly.

#### 8. Path Compression vs Union by Size — Must Know

They solve related but different problems:

```text id="pc20"
Path Compression
      ↓
Optimizes find()
      ↓
Flattens paths during traversal


Union by Size / Rank
      ↓
Optimizes union()
      ↓
Prevents deep trees when merging
```

Best practice:

```text id="pc21"
Path Compression
      +
Union by Size / Rank
```

Use both together.

#### 9. Common Mistakes

1. Returning the root without updating `parent[x]`.

Wrong:

```kotlin id="pc22"
return find(parent[x])
```

Better:

```kotlin id="pc23"
parent[x] = find(parent[x])
return parent[x]
```

2. Thinking Path Compression changes which nodes belong to the component.

It only changes the **internal tree structure**, not connectivity.

3. Saying every individual operation is strictly `O(1)`.

More accurate:

```text id="pc24"
Amortized → O(α(N))
Practically → nearly O(1)
```

#### 10. Interview Must Remember

1. Path Compression is a **DSU optimization**.
2. It happens during `find()`.
3. It connects visited nodes directly/closer to the root.
4. Key line:

```kotlin id="pc25"
parent[x] = find(parent[x])
```

5. It makes future `find()` operations faster.
6. Combine it with **Union by Rank/Size**.
7. Optimized DSU → `O(α(N))` amortized per operation.