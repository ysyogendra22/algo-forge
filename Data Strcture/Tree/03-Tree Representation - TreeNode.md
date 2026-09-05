# Tree Representation / TreeNode

#### 1. Definition — Must Know

1. A **TreeNode** represents one element of a tree.
2. Each node stores a **value** and references to its **child nodes**.
3. The entire tree is accessed through a reference to the **root node**.

#### 2. Why It Is Used — Must Know

1. Represents hierarchical relationships between objects.
2. Child references connect individual nodes to form the complete tree.
3. Most tree interview problems provide or expect a `TreeNode` structure.

#### 3. How It Works — Must Know

```text
        10
       /  \
      5    20
     / \
    3   7
```

Representation:

```text
root → 10

10.left  → 5
10.right → 20

5.left   → 3
5.right  → 7

3.left/right  → null
7.left/right  → null
20.left/right → null
```

1. `root` holds the reference to the first node.
2. Each node holds references to its children.
3. `null` means that child does not exist.
4. Following child references allows us to reach the entire tree.

#### 4. Binary Tree Representation — Must Know

```kotlin
class TreeNode(
    val value: Int,
    var left: TreeNode? = null,
    var right: TreeNode? = null
)
```

1. `value` → Data stored in the node.
2. `left` → Reference to the left child.
3. `right` → Reference to the right child.
4. Nullable references allow a node to have `0`, `1`, or `2` children.

#### 5. Creating a Binary Tree — Must Know

```kotlin
val root = TreeNode(10)

root.left = TreeNode(5)
root.right = TreeNode(20)

root.left?.left = TreeNode(3)
root.left?.right = TreeNode(7)
```

Creates:

```text
        10
       /  \
      5    20
     / \
    3   7
```

#### 6. General / N-ary Tree Representation — Good to Know

When a node can have more than two children:

```kotlin
class TreeNode(
    val value: Int,
    val children: MutableList<TreeNode> = mutableListOf()
)
```

Instead of fixed `left` and `right` references, each node maintains a collection of children.

#### 7. Key Points — Must Know

1. A tree is usually represented using **nodes connected by references**.
2. `root` is the entry point to the entire tree.
3. Binary Tree node → `value + left + right`.
4. Missing children are represented by `null`.
5. N-ary Tree node → `value + collection of children`.
6. Creating/accessing a node or child reference → `O(1)`.
7. Visiting the entire tree requires traversal → `O(n)`.