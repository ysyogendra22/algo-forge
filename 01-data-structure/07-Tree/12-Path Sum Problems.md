# Path Sum Problems

#### 1. Definition — Must Know

1. **Path Sum** problems ask whether or which paths in a tree satisfy a target sum.
2. The most common version checks a **root-to-leaf path** whose values add up to `targetSum`.

#### 2. How It Works — Must Know

```text id="w2fs8m"
        5
       / \
      4   8
     /   / \
    11  13  4
   /  \
  7    2
```

Target = `22`

```text id="mz2p7c"
5 → 4 → 11 → 2

5 + 4 + 11 + 2 = 22
```

Therefore, a valid path exists.

#### 3. Core Logic — Must Know

Use **DFS** and subtract the current value from the remaining target.

```text id="x8n3qp"
remaining = target - node.value
```

At a leaf:

```text id="u5cx7v"
remaining == leaf.value → Valid path
```

Logic:

```text id="d4rj8k"
1. Start from root.
2. Subtract current node value.
3. DFS into left and right children.
4. At a leaf, check whether remaining sum matches.
5. Return true if either subtree finds a valid path.
```

#### 4. Path Sum I — Must Know

**Question:** Does a valid root-to-leaf path exist?

```kotlin id="r7nk4d"
fun hasPathSum(root: TreeNode?, targetSum: Int): Boolean {
    if (root == null) return false

    if (root.left == null && root.right == null) {
        return targetSum == root.value
    }

    val remaining = targetSum - root.value

    return hasPathSum(root.left, remaining) ||
           hasPathSum(root.right, remaining)
}
```

#### 5. Path Sum II — Must Know

**Question:** Return all root-to-leaf paths matching the target.

Use **DFS + Backtracking**.

```kotlin id="h3cf6w"
fun pathSum(root: TreeNode?, targetSum: Int): List<List<Int>> {
    val result = mutableListOf<List<Int>>()
    val path = mutableListOf<Int>()

    fun dfs(node: TreeNode?, remaining: Int) {
        if (node == null) return

        path.add(node.value)

        if (node.left == null &&
            node.right == null &&
            remaining == node.value) {
            result.add(path.toList())
        }

        dfs(node.left, remaining - node.value)
        dfs(node.right, remaining - node.value)

        path.removeAt(path.lastIndex)
    }

    dfs(root, targetSum)

    return result
}
```

#### 6. Backtracking Pattern — Must Know

When maintaining the current path:

```text id="r4ym2b"
Choose
  ↓
Explore
  ↓
Undo
```

In code:

```text id="e9wv7k"
path.add(node)

DFS children

path.removeLast()
```

The **undo** step is critical because the same path list is reused across branches.

#### 7. Important Path Sum Variants — Good to Know

1. **Root → Leaf** — Most basic version.
2. **Root → Any Node** — Path can end before a leaf.
3. **Any Node → Any Descendant** — Often solved using prefix-sum techniques.
4. **Maximum Path Sum** — Different pattern; usually studied separately.

#### 8. Complexity & Key Points — Must Know

1. Path Sum I time → `O(n)`.
2. DFS recursion space → `O(h)`.
3. Returning all paths requires additional space for the output.
4. Path Sum I → **DFS + remaining sum**.
5. Path Sum II → **DFS + backtracking**.
6. Check for a **leaf explicitly** when the problem requires root-to-leaf paths.
7. Don't return true merely because the running sum reaches the target at a non-leaf.
8. Negative values can exist, so don't assume the remaining sum must always decrease toward zero.