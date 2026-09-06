# Binary Search Tree (BST)

#### 1. Definition — Must Know

1. A **Binary Search Tree (BST)** is a Binary Tree with an ordering rule.
2. For every node:
   - Left subtree values `< node`
   - Right subtree values `> node`
3. Both left and right subtrees must also satisfy the BST property.

#### 2. Why It Is Used — Must Know

1. Supports efficient **search, insert, and delete** when the tree is balanced.
2. Keeps data in sorted order.
3. Useful when both **ordered data and dynamic updates** are required.

#### 3. How It Works — Must Know

```text
        8
       / \
      3   10
     / \    \
    1   6    14
       / \   /
      4   7 13
```

To search for `7`:

```text
7 < 8  → Go Left
7 > 3  → Go Right
7 > 6  → Go Right
7 = 7  → Found
```

BST avoids searching both subtrees because the ordering tells us which direction to follow.

#### 4. Core Properties — Must Know

1. Every node has at most **two children**.
2. All values in the left subtree are smaller than the node.
3. All values in the right subtree are greater than the node.
4. **Inorder traversal** of a BST produces values in sorted order.
5. Minimum value → leftmost node.
6. Maximum value → rightmost node.
7. Duplicate handling depends on the problem/design; don't assume a rule.

#### 5. Search — Must Know

```kotlin
fun search(root: TreeNode?, target: Int): TreeNode? {
    if (root == null || root.value == target) {
        return root
    }

    return if (target < root.value) {
        search(root.left, target)
    } else {
        search(root.right, target)
    }
}
```

Logic:

```text
target == node → Found
target < node  → Search Left
target > node  → Search Right
```

#### 6. Insert — Must Know

```kotlin
fun insert(root: TreeNode?, value: Int): TreeNode {
    if (root == null) return TreeNode(value)

    if (value < root.value) {
        root.left = insert(root.left, value)
    } else if (value > root.value) {
        root.right = insert(root.right, value)
    }

    return root
}
```

1. Compare value with current node.
2. Smaller → move left.
3. Larger → move right.
4. Insert when a `null` position is found.

#### 7. Delete — Must Know Concept

Deletion has **3 cases**:

```text
1. Leaf Node
   → Remove directly.

2. One Child
   → Replace node with its child.

3. Two Children
   → Replace with inorder successor/predecessor.
   → Delete that replacement node.
```

For interviews, understand these three cases clearly. Implement deletion separately when practicing BST operations.

#### 8. Inorder Traversal — Must Know

```kotlin
fun inorder(root: TreeNode?) {
    if (root == null) return

    inorder(root.left)
    println(root.value)
    inorder(root.right)
}
```

For the example BST:

```text
1 → 3 → 4 → 6 → 7 → 8 → 10 → 13 → 14
```

This sorted-order property is heavily used in BST interview problems.

#### 9. Complexity & Key Points — Must Know

```text
Operation    Balanced BST    Skewed BST

Search       O(log n)        O(n)
Insert       O(log n)        O(n)
Delete       O(log n)        O(n)
```

1. Complexity depends on tree **height `h`** → operations are generally `O(h)`.
2. Balanced BST → height ≈ `log n`.
3. Skewed BST → height can become `n`.
4. BST does **not automatically mean balanced**.
5. Inorder traversal → `O(n)` and returns sorted values.
6. Search uses the BST property to choose **one subtree**, unlike a general Binary Tree.
7. Remember the core rule: **Left < Root < Right**.
8. For validation, the rule applies to the **entire subtree**, not just immediate children.