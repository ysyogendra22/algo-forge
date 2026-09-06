# Search / Insert / Delete in BST

#### 1. Core Idea — Must Know

BST operations use the ordering property:

```text id="b71p2x"
Left < Root < Right
```

1. Smaller value → move **left**.
2. Larger value → move **right**.
3. This eliminates one subtree at each step when searching/inserting.

#### 2. Search — Must Know

Find a target value in the BST.

```text id="cn83qv"
        8
       / \
      3   10
     / \
    1   6
```

Search `6`:

```text id="p72fgr"
6 < 8 → Left
6 > 3 → Right
6 = 6 → Found
```

Kotlin:

```kotlin id="x92gsa"
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

#### 3. Insert — Must Know

Insert the value where a `null` child is found while maintaining BST order.

```text id="m9r2fc"
Insert 5:

        8
       /
      3
       \
        6
       /
      5
```

Kotlin:

```kotlin id="x31fqd"
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

#### 4. Delete — Must Know

Deletion has **3 cases**.

**Case 1 — Leaf Node**

```text id="w2z78a"
    5
   /
  3

Delete 3

    5
```

Simply remove the node.

**Case 2 — One Child**

```text id="y7f0qs"
    5
     \
      8
       \
        10

Delete 8

    5
     \
      10
```

Replace the deleted node with its child.

**Case 3 — Two Children**

```text id="4k8b3v"
       8
      / \
     3   10
        /  \
       9    12
```

Delete `8`:

1. Find the **inorder successor** → smallest value in right subtree (`9`).
2. Replace `8` with `9`.
3. Delete the original `9`.

```text id="6mbc1q"
       9
      / \
     3   10
           \
            12
```

#### 5. Delete Implementation — Must Know

```kotlin id="v42fxc"
fun delete(root: TreeNode?, value: Int): TreeNode? {
    if (root == null) return null

    when {
        value < root.value ->
            root.left = delete(root.left, value)

        value > root.value ->
            root.right = delete(root.right, value)

        else -> {
            // No left child
            if (root.left == null) return root.right

            // No right child
            if (root.right == null) return root.left

            // Two children
            val successor = findMin(root.right!!)
            root.value = successor.value
            root.right = delete(root.right, successor.value)
        }
    }

    return root
}

fun findMin(root: TreeNode): TreeNode {
    var current = root

    while (current.left != null) {
        current = current.left!!
    }

    return current
}
```

> For this implementation, `TreeNode.value` must be declared as `var`, not `val`.

```kotlin id="q2m8dv"
class TreeNode(
    var value: Int,
    var left: TreeNode? = null,
    var right: TreeNode? = null
)
```

#### 6. Min / Max — Must Know

```text id="k51xmc"
Minimum → Keep moving left.
Maximum → Keep moving right.
```

```kotlin id="n6hp29"
fun findMin(root: TreeNode): TreeNode {
    var current = root

    while (current.left != null) {
        current = current.left!!
    }

    return current
}
```

#### 7. Complexity & Key Points — Must Know

```text id="v38dm4"
Operation    Balanced     Skewed

Search       O(log n)     O(n)
Insert       O(log n)     O(n)
Delete       O(log n)     O(n)
Min / Max    O(log n)     O(n)
```

1. More generally, Search / Insert / Delete → `O(h)`.
2. BST is **not automatically balanced**.
3. Search → compare and choose one subtree.
4. Insert → find the correct `null` position.
5. Delete → remember **0 child, 1 child, 2 children**.
6. Two-child deletion commonly uses the **inorder successor** or **inorder predecessor**.
7. Inorder successor for this case → smallest node in the **right subtree**.
8. Preserve the BST property after every modification.