# Tree Views

#### 1. Definition — Must Know

1. **Tree View** means the nodes visible when a Binary Tree is observed from a particular direction.
2. For FAANG-style interviews, **Right Side View** and **Left Side View** are the main ones to know.

#### 2. How It Works — Must Know

```text id="tv001a"
        1
       / \
      2   3
       \   \
        5   4
```

```text id="tv002a"
Left View  → 1, 2, 5
Right View → 1, 3, 4
```

Think **one visible node per level**.

#### 3. Right Side View — Must Know

Using BFS:

```text id="tv003a"
1. Traverse level by level.
2. Process all nodes of the current level.
3. Take the last node of each level.
```

Kotlin:

```kotlin id="tv004a"
fun rightSideView(root: TreeNode?): List<Int> {
    if (root == null) return emptyList()

    val result = mutableListOf<Int>()
    val queue = ArrayDeque<TreeNode>()
    queue.addLast(root)

    while (queue.isNotEmpty()) {
        val levelSize = queue.size

        repeat(levelSize) { index ->
            val node = queue.removeFirst()

            if (index == levelSize - 1) {
                result.add(node.value)
            }

            node.left?.let { queue.addLast(it) }
            node.right?.let { queue.addLast(it) }
        }
    }

    return result
}
```

#### 4. Left Side View — Must Know

Same BFS pattern, but take the **first node** of each level.

```kotlin id="tv005a"
fun leftSideView(root: TreeNode?): List<Int> {
    if (root == null) return emptyList()

    val result = mutableListOf<Int>()
    val queue = ArrayDeque<TreeNode>()
    queue.addLast(root)

    while (queue.isNotEmpty()) {
        val levelSize = queue.size

        repeat(levelSize) { index ->
            val node = queue.removeFirst()

            if (index == 0) {
                result.add(node.value)
            }

            node.left?.let { queue.addLast(it) }
            node.right?.let { queue.addLast(it) }
        }
    }

    return result
}
```

#### 5. DFS Approach — Good to Know

Tree views can also be solved using **depth**.

For Right View:

```text id="tv006a"
1. Visit Root → Right → Left.
2. Track current depth.
3. First node encountered at each new depth is visible.
```

For Left View:

```text id="tv007a"
Root → Left → Right
```

BFS is usually easier to recognize because tree views naturally map to **levels**.

#### 6. Other Views — Good to Know

1. **Top View** — First visible node at each horizontal distance.
2. **Bottom View** — Last visible node at each horizontal distance.
3. **Vertical Order Traversal** — Group nodes by horizontal position.

These require tracking more information than simple left/right views and can be studied separately if needed.

#### 7. Complexity & Key Points — Must Know

1. Time → `O(n)` — every node is visited once.
2. BFS space → `O(w)` where `w` is maximum tree width.
3. Right View → last node of each BFS level.
4. Left View → first node of each BFS level.
5. Tree Views are primarily a **level-order/BFS pattern**.
6. Don't confuse **Right Side View** with simply following `right` pointers; a visible node can come from a left subtree when no node blocks it on that level.