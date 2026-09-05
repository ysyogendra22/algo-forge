# DFS Traversal

#### 1. Definition — Must Know

1. **DFS (Depth-First Search)** explores one branch of a tree as deep as possible before backtracking.
2. DFS is commonly implemented using **recursion** or a **stack**.

#### 2. Why It Is Used — Must Know

1. Traverse or search the entire tree.
2. Solve path and subtree problems.
3. Calculate height, depth, diameter, and other subtree-based results.
4. Useful when a problem requires exploring descendants before moving to another branch.

#### 3. How It Works — Must Know

```text
        1
       / \
      2   3
     / \
    4   5
```

Example DFS:

```text
1 → 2 → 4 → 5 → 3
```

1. Start at the root `1`.
2. Move to `2`.
3. Continue deeper to `4`.
4. No child → backtrack to `2`.
5. Visit `5`.
6. Backtrack and continue with `3`.

#### 4. DFS Traversal Types — Must Know

1. **Preorder** → Root → Left → Right

```text
1 → 2 → 4 → 5 → 3
```

2. **Inorder** → Left → Root → Right

```text
4 → 2 → 5 → 1 → 3
```

3. **Postorder** → Left → Right → Root

```text
4 → 5 → 2 → 3 → 1
```

#### 5. Recursive Implementation — Must Know

```kotlin
fun dfs(root: TreeNode?) {
    if (root == null) return

    println(root.value)

    dfs(root.left)
    dfs(root.right)
}
```

1. `root == null` → Base case.
2. Process current node.
3. Explore left subtree.
4. Explore right subtree.
5. Recursion automatically handles backtracking.

#### 6. Iterative Implementation — Must Know

```kotlin
fun dfs(root: TreeNode?) {
    if (root == null) return

    val stack = ArrayDeque<TreeNode>()
    stack.addLast(root)

    while (stack.isNotEmpty()) {
        val node = stack.removeLast()

        println(node.value)

        node.right?.let { stack.addLast(it) }
        node.left?.let { stack.addLast(it) }
    }
}
```

1. DFS uses a **LIFO stack**.
2. Push `right` first so `left` is processed first.
3. Recursive DFS uses the **call stack** internally.

#### 7. Common DFS Patterns — Must Know

1. **Top-Down DFS** — Pass information from parent → child.
   - Path Sum
   - Current depth
   - Root-to-leaf paths

2. **Bottom-Up DFS** — Return information from child → parent.
   - Tree height
   - Balanced tree
   - Diameter
   - Maximum path sum

3. **Search DFS** — Explore recursively until a required node/value is found.

#### 8. When to Use Pre/In/Postorder — Must Know

1. **Preorder** → Need to process parent before children.
2. **Inorder** → Important for BST; gives values in sorted order.
3. **Postorder** → Need child/subtree results before processing parent.

#### 9. Complexity & Interview Points — Must Know

1. Time → `O(n)` because each node is visited once.
2. Space → `O(h)` where `h` is tree height.
3. Balanced tree → `O(log n)` recursion/stack space.
4. Skewed tree → `O(n)` recursion/stack space.
5. Always handle `root == null`.
6. Recursive DFS is usually simplest for tree interview problems.
7. Iterative DFS is useful when recursion depth may become too large.
8. DFS is usually preferred over BFS when solving **path, subtree, height, or recursive dependency** problems.