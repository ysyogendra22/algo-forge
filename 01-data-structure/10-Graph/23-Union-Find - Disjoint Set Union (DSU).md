# Union-Find / Disjoint Set Union (DSU)

#### 1. Definition — Must Know

1. **Union-Find / DSU** manages elements divided into separate connected groups.
2. It efficiently answers:

```text
Are A and B connected?
```

3. Two main operations:

```text
Find  → Find which group an element belongs to.
Union → Merge two groups.
```

#### 2. Why It Is Used — Must Know

DSU is useful when the problem involves:

```text
Connections + Merging Groups
```

Common uses:

1. Connected Components.
2. Dynamic connectivity.
3. Cycle Detection — Undirected Graph.
4. Kruskal's Minimum Spanning Tree.
5. Accounts Merge.

#### 3. Core Concept — Must Know

Initially every node belongs to its own group.

```text
0   1   2   3   4
```

Parent:

```text
parent = [0, 1, 2, 3, 4]
```

After:

```text
union(0, 1)
union(1, 2)
```

We may have:

```text
    0
   / \
  1   2

3

4
```

Now:

```text
find(0) == find(2)
```

So `0` and `2` belong to the same component.

#### 4. Find Operation — Must Know

`find(x)` returns the **root / representative** of the group containing `x`.

Example:

```text
2 → 1 → 0
```

Then:

```text
find(2) = 0
find(1) = 0
find(0) = 0
```

If:

```text
find(a) == find(b)
```

then `a` and `b` are connected.

#### 5. Union Operation — Must Know

To merge `a` and `b`:

```text
rootA = find(a)
rootB = find(b)
```

If:

```text
rootA != rootB
```

merge the two groups.

Conceptually:

```text
Before:

0 --- 1

2 --- 3


union(1, 2)


After:

0 --- 1 --- 2 --- 3
```

#### 6. Basic Implementation

A basic DSU can do:

```kotlin
fun find(x: Int): Int {

    if (parent[x] == x) {
        return x
    }

    return find(parent[x])
}
```

But this can create deep trees:

```text
4 → 3 → 2 → 1 → 0
```

which makes `find()` slower.

Two optimizations are important:

```text
Path Compression
Union by Rank / Size
```

#### 7. Path Compression — Must Know

Without compression:

```text
4 → 3 → 2 → 1 → 0
```

After:

```text
find(4)
```

Path compression changes it closer to:

```text
    0
  / | | \
 1  2 3  4
```

Implementation:

```kotlin
fun find(x: Int): Int {

    if (parent[x] != x) {
        parent[x] = find(parent[x])
    }

    return parent[x]
}
```

Key line:

```kotlin
parent[x] = find(parent[x])
```

This makes future `find()` operations very fast.

#### 8. Union by Rank / Size — Must Know

Goal:

```text
Avoid creating deep trees.
```

With **Union by Size**, attach the smaller tree under the larger tree.

```text
Small Tree
    ↓
Large Tree
```

This keeps the DSU structure shallow.

You only need to implement **Rank or Size** in an interview, not both.

#### 9. Kotlin Implementation — Must Know

Using:

```text
Path Compression + Union by Size
```

```kotlin
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

Usage:

```kotlin
val dsu = DSU(5)

dsu.union(0, 1)
dsu.union(1, 2)

println(dsu.find(0) == dsu.find(2))
// true
```

#### 10. Why `union()` Returns Boolean — Good to Know

Our implementation returns:

```text
true  → Two different components were merged.

false → They were already connected.
```

This is very useful for **cycle detection**.

#### 11. Cycle Detection — Must Know

For every undirected edge:

```text
(u, v)
```

Check:

```text
find(u) == find(v)
```

If true:

```text
Already Connected
       ↓
Adding this edge
       ↓
Creates Cycle
```

Example:

```text
0 ----- 1
 \     /
   \ /
    2
```

Process:

```text
union(0,1) → true
union(1,2) → true
union(0,2) → false
```

The last edge detects the cycle.

#### 12. Connected Components — Must Know

Initially:

```text
components = n
```

Every successful union:

```text
components--
```

Example:

```kotlin
var components = n

for ((u, v) in edges) {

    if (dsu.union(u, v)) {
        components--
    }
}
```

Final value gives the number of connected components.

#### 13. Time & Space Complexity — Must Know

With:

```text
Path Compression
+
Union by Rank / Size
```

Each operation is approximately:

```text
Find  → O(α(N))
Union → O(α(N))
```

`α(N)` = inverse Ackermann function.

Practically:

```text
O(α(N)) ≈ O(1)
```

Space:

```text
O(N)
```

For interviews, remember:

```text
Optimized DSU operations are nearly O(1).
```

#### 14. DFS/BFS vs DSU — Must Know

```text
DFS / BFS                   DSU

Traverse graph              Merge components
Explore neighbors           Process connections
O(V + E) traversal          Near O(1) per operation
Great for graph search      Great for connectivity
Can find paths              Does not give actual path
```

Think:

```text
Need traversal/path
      ↓
   BFS / DFS

Need repeated connectivity/merging
      ↓
      DSU
```

#### 15. Common Interview Patterns — Must Know

1. **Are two nodes connected?**
   ```text
   find(a) == find(b)
   ```

2. **Merge groups**
   ```text
   union(a, b)
   ```

3. **Count components**
   ```text
   components--
   ```

4. **Undirected cycle detection**
   ```text
   union() fails → Cycle
   ```

5. **Minimum Spanning Tree**
   ```text
   Kruskal + DSU
   ```

#### 16. Common Mistakes — Must Know

1. Forgetting path compression.
2. Forgetting Union by Rank/Size optimization.
3. Comparing `parent[a] == parent[b]` instead of `find(a) == find(b)`.
4. Decreasing component count even when union fails.
5. Using DSU when the actual path/traversal is required.
6. Using basic DSU cycle logic directly for directed graphs.

#### 17. Interview Must Remember

1. DSU = **manage connected groups efficiently**.
2. `find(x)` → find group representative.
3. `union(a,b)` → merge groups.
4. `find(a) == find(b)` → already connected.
5. Use **Path Compression + Union by Rank/Size**.
6. Optimized operations → practically `O(1)`.
7. **Connectivity + repeated merging → think DSU**.