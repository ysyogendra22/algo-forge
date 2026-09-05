#treebasics
# Tree Basics

#### 1. Definition — Must Know

1. A **Tree** is a non-linear data structure used to represent hierarchical data.

2. It consists of **nodes** connected by **edges**.

3. The topmost node is called the **root**.

4. A tree with `N` nodes has `N - 1` edges.


#### 2. Why It Is Used — Must Know

1. Represents **parent-child relationships** naturally.

2. Makes hierarchical data easier to organize, search, and process.

3. Common examples: file systems, DOM, organization hierarchy, database indexes.


#### 3. How It Works — Must Know

```text
        1
      /   \
     2     3
    / \
   4   5
```

1. `1` → Root.

2. `2, 3` → Children of `1`.

3. `4, 5` → Children of `2`.

4. `3, 4, 5` → Leaf nodes.

5. `2, 4, 5` → Form a subtree.


#### 4. Core Concepts — Must Know

1. **Node** — Stores data.

2. **Edge** — Connection between nodes.

3. **Root** — Topmost node.

4. **Parent** — Node directly above another node.

5. **Child** — Node directly below another node.

6. **Sibling** — Nodes with the same parent.

7. **Leaf** — Node with no children.

8. **Subtree** — Node and all its descendants.

9. **Ancestor** — Node above another node in its path to the root.

10. **Descendant** — Node below another node.

11. **Depth** — Number of edges from root to a node.

12. **Height** — Longest path from a node to a leaf.


#### 5. Basic Properties — Must Know

1. A tree is **connected** and has **no cycles**.

2. There is exactly **one path** between any two nodes.

3. `N` nodes → `N - 1` edges.

4. Traversing all nodes → `O(n)`.

5. Searching an unordered tree → `O(n)`.

6. Don't assume tree search is `O(log n)` — it depends on the tree type.

7. An empty tree can have `root = null`.

8. A single-node tree has the root as a **leaf**.

9. Don't confuse **Tree**, **Binary Tree**, and **Binary Search Tree**.


#### 6. Interview Must Remember

1. Tree = hierarchical **nodes + edges**.

2. `N` nodes → `N - 1` edges.

3. Trees are **connected and acyclic**.

4. Understand **root, parent, child, leaf, subtree, depth, and height**.

5. Tree traversal commonly uses **DFS or BFS**.

6. General tree operations are not automatically `O(log n)`.

7. **Tree → Binary Tree → BST** are different concepts; don't use the terms interchangeably.

#### 7. Basic Representation — Must Know

```kotlin
class TreeNode(
    val value: Int,
    var left: TreeNode? = null,
    var right: TreeNode? = null
)
```