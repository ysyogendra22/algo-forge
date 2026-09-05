# BFS / Level Order Traversal

#### 1. Definition — Must Know

1. **BFS (Breadth-First Search)** traverses a tree **level by level**.
2. It visits all nodes at the current level before moving to the next level.
3. BFS is commonly implemented using a **Queue**.

#### 2. Why It Is Used — Must Know

1. Process nodes level by level.
2. Find minimum depth / shortest path in an unweighted structure.
3. Solve problems involving tree levels, width, or views.
4. Useful when the **nearest node/result** matters.

#### 3. How It Works — Must Know

```text
        1
       / \
      2   3
     / \
    4   5
```

BFS traversal:

```text
1 → 2 → 3 → 4 → 5
```

1. Add root `1` to the queue.
2. Remove `1` → add `2, 3`.
3. Remove `2` → add `4, 5`.
4. Remove `3`.
5. Remove `4`, then `5`.
6. Continue until the queue is empty.

#### 4. Core Logic — Must Know

```text
Queue = [root]

while Queue is not empty:
    remove first node
    process node
    add its children to Queue
```

1. Queue follows **FIFO**.
2. Nodes are added at the end.
3. Nodes are processed from the front.

#### 5. Basic BFS Implementation — Must Know

```kotlin
fun bfs(root: TreeNode?) {
    if (root == null) return

    val queue = ArrayDeque<TreeNode>()
    queue.addLast(root)

    while (queue.isNotEmpty()) {
        val node = queue.removeFirst()

        println(node.value)

        node.left?.let { queue.addLast(it) }
        node.right?.let { queue.addLast(it) }
    }
}
```

#### 6. Level-by-Level Implementation — Must Know

Use `queue.size` to know how many nodes belong to the current level.

```kotlin
fun levelOrder(root: TreeNode?): List<List<Int>> {
    if (root == null) return emptyList()

    val result = mutableListOf<List<Int>>()
    val queue = ArrayDeque<TreeNode>()
    queue.addLast(root)

    while (queue.isNotEmpty()) {
        val levelSize = queue.size
        val level = mutableListOf<Int>()

        repeat(levelSize) {
            val node = queue.removeFirst()

            level.add(node.value)

            node.left?.let { queue.addLast(it) }
            node.right?.let { queue.addLast(it) }
        }

        result.add(level)
    }

    return result
}
```

Result:

```text
[
  [1],
  [2, 3],
  [4, 5]
]
```

#### 7. Common BFS Patterns — Must Know

1. **Level Order** — Process every level separately.
2. **Minimum Depth** — First valid leaf reached gives the minimum depth.
3. **Right/Left Side View** — Take the last/first node of each level.
4. **Zigzag Traversal** — Alternate traversal direction for each level.

#### 8. Complexity & Interview Points — Must Know

1. Time → `O(n)` because every node is visited once.
2. Space → `O(w)` where `w` is the maximum width of the tree.
3. BFS uses a **Queue**; DFS uses a **Stack/recursion**.
4. `queue.size` before processing a level is the key technique for level-based problems.
5. Always handle `root == null`.
6. Use BFS when the problem asks about **levels, nearest nodes, minimum depth, or level views**.
7. Don't use BFS automatically for every tree problem; subtree/path calculations are often simpler with DFS.