# Balanced Binary Tree

#### 1. Definition — Must Know

1. A **Balanced Binary Tree** is a Binary Tree where, for **every node**, the height difference between left and right subtrees is at most `1`.
2. Balance condition:

```text
| leftHeight - rightHeight | <= 1
```

3. The condition must hold for **every node**, not only the root.

#### 2. Why It Matters — Must Know

1. Balanced trees avoid becoming highly skewed.
2. For BSTs, keeping height near `O(log n)` enables efficient search, insert, and delete.
3. An ordinary Binary Tree is **not automatically balanced**.

#### 3. How It Works — Must Know

Balanced:

```text
        1
       / \
      2   3
     / \
    4   5
```

At every node:

```text
|leftHeight - rightHeight| <= 1
```

Unbalanced:

```text
        1
       /
      2
     /
    3
   /
  4
```

At node `1`, the subtree-height difference is greater than `1`.

#### 4. Core Logic — Must Know

Use **bottom-up DFS / Postorder**.

```text
1. Calculate left subtree height.
2. Calculate right subtree height.
3. If difference > 1 → Unbalanced.
4. Otherwise return:
   1 + max(leftHeight, rightHeight)
```

Why bottom-up?

```text
Children's heights
       ↓
Check current node
       ↓
Return current height
```

The parent cannot determine its balance until it knows both child heights.

#### 5. Optimal Kotlin Implementation — Must Know

```kotlin
fun isBalanced(root: TreeNode?): Boolean {
    return height(root) != -1
}

fun height(node: TreeNode?): Int {
    if (node == null) return 0

    val left = height(node.left)
    if (left == -1) return -1

    val right = height(node.right)
    if (right == -1) return -1

    if (kotlin.math.abs(left - right) > 1) {
        return -1
    }

    return 1 + maxOf(left, right)
}
```

Here `-1` means:

```text
This subtree is already unbalanced.
```

This avoids unnecessary further work.

#### 6. Complexity & Key Points — Must Know

1. Time → `O(n)` — each node is processed once.
2. Space → `O(h)` — recursion stack.
3. Balanced tree stack → `O(log n)`.
4. Skewed tree stack → `O(n)`.
5. Check balance at **every node**, not only the root.
6. Use **bottom-up DFS** because the parent depends on child heights.
7. Don't calculate subtree heights repeatedly — a naive solution can become `O(n²)`.
8. **Balanced Binary Tree** describes tree shape; it does not automatically mean **Binary Search Tree**.