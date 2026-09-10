# Union by Rank / Size

#### 1. Definition — Must Know

1. **Union by Rank / Size** is an optimization used in **Union-Find / DSU**.
2. It prevents DSU trees from becoming unnecessarily deep.
3. When merging two components, attach the **smaller/shorter tree under the larger/taller tree**.

```text id="urs01"
Smaller Tree
     ↓
Larger Tree
```

#### 2. Why It Is Needed — Must Know

Without optimization, unions may create a deep tree:

```text id="urs02"
4 → 3 → 2 → 1 → 0
```

Deep trees make:

```text id="urs03"
find()
```

slower.

Union by Rank/Size keeps the tree shallow.

#### 3. Union by Size — Must Know

`size[root]` stores the number of nodes in that component.

Example:

```text id="urs04"
Component A        Component B

    0                  3
   / \                 |
  1   2                4

Size = 3           Size = 2
```

When merging:

```text id="urs05"
union(0, 3)
```

Attach the smaller component under the larger:

```text id="urs06"
      0
    / | \
   1  2  3
         |
         4
```

Then:

```text id="urs07"
size[0] = 3 + 2 = 5
```

#### 4. Union by Size Logic — Must Know

```text id="urs08"
1. Find rootA.
2. Find rootB.
3. If same root → already connected.
4. Compare their sizes.
5. Attach smaller root under larger root.
6. Update size of larger component.
```

#### 5. Kotlin — Union by Size — Recommended

```kotlin id="urs09"
class DSU(n: Int) {

    private val parent = IntArray(n) { it }
    private val size = IntArray(n) { 1 }

    fun find(x: Int): Int {

        if (parent[x] != x) {
            parent[x] = find(parent[x])
        }

        return parent[x]
    }

    fun union(a: Int, b: Int): Boolean {

        var rootA = find(a)
        var rootB = find(b)

        if (rootA == rootB) {
            return false
        }

        if (size[rootA] < size[rootB]) {
            val temp = rootA
            rootA = rootB
            rootB = temp
        }

        parent[rootB] = rootA
        size[rootA] += size[rootB]

        return true
    }
}
```

Important part:

```kotlin id="urs10"
if (size[rootA] < size[rootB]) {
    val temp = rootA
    rootA = rootB
    rootB = temp
}

parent[rootB] = rootA
size[rootA] += size[rootB]
```

#### 6. Union by Rank — Must Know

`rank` represents an estimate of the tree's **height/depth**.

Rule:

```text id="urs11"
Lower Rank
    ↓
Higher Rank
```

If both ranks are equal:

```text id="urs12"
Attach one under the other
          ↓
Increase new root's rank by 1
```

#### 7. Kotlin — Union by Rank

```kotlin id="urs13"
class DSU(n: Int) {

    private val parent = IntArray(n) { it }
    private val rank = IntArray(n)

    fun find(x: Int): Int {

        if (parent[x] != x) {
            parent[x] = find(parent[x])
        }

        return parent[x]
    }

    fun union(a: Int, b: Int): Boolean {

        val rootA = find(a)
        val rootB = find(b)

        if (rootA == rootB) {
            return false
        }

        if (rank[rootA] < rank[rootB]) {

            parent[rootA] = rootB

        } else if (rank[rootA] > rank[rootB]) {

            parent[rootB] = rootA

        } else {

            parent[rootB] = rootA
            rank[rootA]++
        }

        return true
    }
}
```

#### 8. Rank vs Size — Must Know

```text id="urs14"
Union by Size              Union by Rank

Tracks node count          Tracks tree height/rank
size[root]                 rank[root]

Smaller → Larger           Shorter → Taller

Update size after merge    Increase rank only
                           when ranks are equal
```

Both solve the same main problem:

```text id="urs15"
Keep DSU trees shallow
```

#### 9. Which One Should You Use?

For interviews, choose **one**.

Recommended:

```text id="urs16"
Path Compression
      +
Union by Size
```

Why?

1. Easy to understand.
2. Easy to implement.
3. Size can also tell you how many nodes are in a component.
4. Same practical performance as Union by Rank.

You do **not** need to implement both Rank and Size together.

#### 10. Path Compression vs Union by Rank/Size

```text id="urs17"
Path Compression
      ↓
Optimizes find()
      ↓
Flattens existing paths


Union by Rank/Size
      ↓
Optimizes union()
      ↓
Prevents deep paths from forming
```

Best combination:

```text id="urs18"
Path Compression
        +
Union by Rank / Size
        ↓
Efficient DSU
```

#### 11. Complexity — Must Know

With:

```text id="urs19"
Path Compression
+
Union by Rank / Size
```

amortized complexity:

```text id="urs20"
Find  → O(α(N))
Union → O(α(N))
```

Practically:

```text id="urs21"
≈ O(1)
```

Space:

```text id="urs22"
O(N)
```

#### 12. Common Mistakes — Must Know

1. Comparing `size[a]` and `size[b]` instead of their roots.

Correct:

```kotlin id="urs23"
val rootA = find(a)
val rootB = find(b)
```

2. Updating size on the wrong root.

3. Increasing rank after every union.

Rank increases only when:

```text id="urs24"
rank[rootA] == rank[rootB]
```

4. Using both Rank and Size unnecessarily.

5. Forgetting Path Compression in `find()`.

#### 13. Interview Must Remember

1. Union by Rank/Size is a **DSU optimization**.
2. Goal → keep trees **shallow**.
3. Size → attach **smaller component under larger**.
4. Rank → attach **lower-rank tree under higher-rank tree**.
5. If ranks are equal → merge and increment the new root's rank.
6. Use **Rank OR Size**, not both.
7. Recommended interview implementation → **Path Compression + Union by Size**.
8. Optimized DSU operations → `O(α(N))` amortized.