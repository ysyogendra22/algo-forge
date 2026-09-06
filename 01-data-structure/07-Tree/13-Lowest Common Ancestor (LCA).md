# Lowest Common Ancestor (LCA)

#### 1. Definition — Must Know

1. **Lowest Common Ancestor (LCA)** is the lowest node in a tree that has both given nodes as descendants.
2. A node can be considered a descendant of **itself**.

#### 2. How It Works — Must Know

```text id="lca01x"
        3
       / \
      5   1
     / \
    6   2
       / \
      7   4
```

Examples:

```text id="lca02x"
LCA(6, 4) → 5
LCA(5, 4) → 5
LCA(6, 1) → 3
```

The goal is to find the **deepest node where the paths to both nodes meet**.

#### 3. Core Logic — Binary Tree — Must Know

Use **bottom-up DFS**.

```text id="lca03x"
1. If node == null → return null.
2. If node == p or q → return node.
3. Search left subtree.
4. Search right subtree.
5. If both return non-null → current node is LCA.
6. Otherwise return whichever side is non-null.
```

Key idea:

```text id="lca04x"
left != null AND right != null
            ↓
     Current Node = LCA
```

#### 4. Kotlin Implementation — Must Know

```kotlin id="lca05x"
fun lowestCommonAncestor(
    root: TreeNode?,
    p: TreeNode,
    q: TreeNode
): TreeNode? {

    if (root == null || root == p || root == q) {
        return root
    }

    val left = lowestCommonAncestor(root.left, p, q)
    val right = lowestCommonAncestor(root.right, p, q)

    if (left != null && right != null) {
        return root
    }

    return left ?: right
}
```

#### 5. Why It Works — Must Know

Consider:

```text id="lca06x"
        5
       / \
      6   2
           \
            4
```

For `6` and `4`:

```text id="lca07x"
Left subtree  → finds 6
Right subtree → finds 4

Both found
    ↓
Node 5 is LCA
```

If both target nodes are inside the same subtree, that subtree returns their LCA upward.

#### 6. LCA in BST — Must Know

BST ordering allows a simpler solution.

```text id="lca08x"
p and q < root → Go Left

p and q > root → Go Right

Otherwise      → Root is LCA
```

Kotlin:

```kotlin id="lca09x"
fun lowestCommonAncestorBST(
    root: TreeNode?,
    p: TreeNode,
    q: TreeNode
): TreeNode? {

    var node = root

    while (node != null) {
        when {
            p.value < node.value && q.value < node.value ->
                node = node.left

            p.value > node.value && q.value > node.value ->
                node = node.right

            else ->
                return node
        }
    }

    return null
}
```

#### 7. Binary Tree vs BST — Must Know

```text id="lca10x"
Binary Tree → DFS both subtrees

BST         → Use ordering to choose direction
```

1. General Binary Tree LCA → `O(n)`.
2. BST LCA → `O(h)`.
3. Balanced BST → `O(log n)`.
4. Skewed BST → `O(n)`.

#### 8. Complexity & Key Points — Must Know

1. Binary Tree LCA time → `O(n)`.
2. Binary Tree recursion space → `O(h)`.
3. LCA is the **lowest/deepest common ancestor**, not simply any common ancestor.
4. If current node equals `p` or `q`, return it.
5. Left and right both find a target → current node is LCA.
6. General Binary Tree → **bottom-up DFS**.
7. BST → exploit **Left < Root < Right** instead of searching the whole tree.
8. The standard Binary Tree implementation usually assumes both target nodes exist in the tree; if existence is not guaranteed, additional validation is required.