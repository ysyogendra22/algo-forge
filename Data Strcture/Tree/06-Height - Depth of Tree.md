# Height / Depth of Tree

#### 1. Definition — Must Know

1. **Depth of a Node** → Distance from the **root to that node**.
2. **Height of a Node** → Longest path from that **node to a leaf**.
3. **Height of Tree** → Height of the root.
4. Depth moves **top → down**; height is calculated **bottom → up**.

#### 2. How It Works — Must Know

```text id="c7dk29"
        1
       / \
      2   3
     /
    4
```

Using **number of edges**:

```text id="n9xr21"
Node    Depth    Height

1         0         2
2         1         1
3         1         0
4         2         0
```

1. Depth of `4` → `2` edges from root.
2. Height of `2` → `1` edge to deepest leaf.
3. Height of tree → `2`.

#### 3. Height vs Depth — Must Know

```text id="bw6ml2"
Depth  → Root → Node
Height → Node → Deepest Leaf
```

1. Root depth → `0`.
2. Leaf height → `0` when counting edges.
3. Maximum depth of a tree is effectively its height when the same counting convention is used.

#### 4. Calculate Maximum Depth — Must Know

Use **bottom-up DFS**:

```text id="v4w0bc"
maxDepth(node):
    if node is null:
        return 0

    left  = maxDepth(node.left)
    right = maxDepth(node.right)

    return 1 + max(left, right)
```

Kotlin:

```kotlin id="0gqhn9"
fun maxDepth(root: TreeNode?): Int {
    if (root == null) return 0

    val left = maxDepth(root.left)
    val right = maxDepth(root.right)

    return 1 + maxOf(left, right)
}
```

> This implementation measures depth/height by **number of nodes**, which is the convention commonly used in coding problems.

#### 5. Calculate Node Depth — Must Know

Use **top-down DFS** and carry the current depth:

```kotlin id="n7n51h"
fun findDepth(
    root: TreeNode?,
    target: Int,
    depth: Int = 0
): Int {
    if (root == null) return -1
    if (root.value == target) return depth

    val left = findDepth(root.left, target, depth + 1)
    if (left != -1) return left

    return findDepth(root.right, target, depth + 1)
}
```

#### 6. Complexity & Key Points — Must Know

1. Maximum depth time → `O(n)` because every node may be visited.
2. DFS recursion space → `O(h)`.
3. Balanced tree → `O(log n)` recursion space.
4. Skewed tree → `O(n)` recursion space.
5. **Depth** is usually carried from parent to child → top-down.
6. **Height** is usually returned from children to parent → bottom-up.
7. Always confirm whether the problem counts **edges or nodes**.
8. `1 + max(left, right)` is one of the most important tree-recursion patterns.