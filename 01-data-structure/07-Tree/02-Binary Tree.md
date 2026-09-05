# Binary Tree

#### 1. Definition — Must Know

1. A **Binary Tree** is a tree where each node can have at most **two children**.
2. The two children are called **left child** and **right child**.
3. A Binary Tree does **not** automatically follow any ordering rule.

#### 2. Why It Is Used — Must Know

1. Represents hierarchical data with at most two branches per node.
2. Forms the foundation for **BST, Heap, AVL Tree, and Red-Black Tree**.
3. Many recursive and tree-based interview problems use Binary Trees.

#### 3. How It Works — Must Know

```text
        1
       / \
      2   3
     / \
    4   5
```

1. `1` → Root.
2. `2` → Left child of `1`.
3. `3` → Right child of `1`.
4. Every node can have `0`, `1`, or `2` children.
5. `4`, `5`, and `3` are leaf nodes.

#### 4. Core Concepts — Must Know

1. **Left Child** — Left branch of a node.
2. **Right Child** — Right branch of a node.
3. **Leaf Node** — Node with no children.
4. **Subtree** — Each child can itself be the root of another Binary Tree.
5. **Height / Depth** — Important for measuring the structure of a tree.

#### 5. Important Types — Must Know

1. **Full Binary Tree** — Every node has either `0` or `2` children.
2. **Complete Binary Tree** — All levels are full except possibly the last, which fills left-to-right.
3. **Perfect Binary Tree** — All internal nodes have `2` children and all leaves are at the same level.
4. **Balanced Binary Tree** — Left and right subtree heights stay reasonably balanced.
5. **Skewed Binary Tree** — Nodes mostly have only one child, behaving similarly to a linked list.

#### 6. Basic Implementation — Must Know

```kotlin
class TreeNode(
    val value: Int,
    var left: TreeNode? = null,
    var right: TreeNode? = null
)
```

Example:

```kotlin
val root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
```

#### 7. Key Points — Must Know

1. Binary Tree → maximum **2 children per node**.
2. Left and right children are **distinct positions**.
3. Binary Tree does **not** mean `left < root < right`; that rule belongs to a **BST**.
4. General Binary Tree search → `O(n)` in the worst case.
5. Traversing all nodes → `O(n)`.
6. Tree shape can range from **balanced to completely skewed**.
7. DFS and BFS are the main ways to traverse a Binary Tree.