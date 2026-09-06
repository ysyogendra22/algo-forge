# Construct Tree from Traversals

#### 1. Definition — Must Know

1. **Construct Tree from Traversals** means rebuilding a Binary Tree using its traversal sequences.
2. The most important interview case is:
   - **Preorder + Inorder**
3. Also know:
   - **Postorder + Inorder**

#### 2. Core Traversal Rules — Must Know

```text id="ct001"
Preorder  → Root → Left → Right
Inorder   → Left → Root → Right
Postorder → Left → Right → Root
```

The key idea:

1. Preorder tells us the **root first**.
2. Postorder tells us the **root last**.
3. Inorder tells us which nodes belong to the **left and right subtrees**.

#### 3. How It Works — Preorder + Inorder

Given:

```text id="ct002"
Preorder → [3, 9, 20, 15, 7]
Inorder  → [9, 3, 15, 20, 7]
```

Step 1 — First preorder value is root:

```text id="ct003"
Root = 3
```

Step 2 — Find `3` in inorder:

```text id="ct004"
[9] | 3 | [15, 20, 7]

Left        Right
```

Step 3 — Recursively build both subtrees.

Result:

```text id="ct005"
        3
       / \
      9   20
         /  \
        15   7
```

#### 4. Core Algorithm — Must Know

For **Preorder + Inorder**:

```text id="ct006"
1. Take next value from preorder → Root.
2. Find root position in inorder.
3. Values left of root → Left subtree.
4. Values right of root → Right subtree.
5. Recursively construct Left.
6. Recursively construct Right.
```

Important:

```text id="ct007"
Build Left before Right
```

because preorder is:

```text id="ct008"
Root → Left → Right
```

#### 5. Optimized Kotlin Implementation — Must Know

```kotlin id="ct009"
fun buildTree(
    preorder: IntArray,
    inorder: IntArray
): TreeNode? {

    val indexMap = mutableMapOf<Int, Int>()

    for (i in inorder.indices) {
        indexMap[inorder[i]] = i
    }

    var preorderIndex = 0

    fun build(left: Int, right: Int): TreeNode? {
        if (left > right) return null

        val rootValue = preorder[preorderIndex++]
        val root = TreeNode(rootValue)

        val inorderIndex = indexMap[rootValue]!!

        root.left = build(left, inorderIndex - 1)
        root.right = build(inorderIndex + 1, right)

        return root
    }

    return build(0, inorder.lastIndex)
}
```

#### 6. Why Use a HashMap? — Must Know

Without a map:

```text id="ct010"
Find root in inorder → O(n)
```

Doing this repeatedly can make construction:

```text id="ct011"
O(n²)
```

With:

```text id="ct012"
value → inorder index
```

lookup becomes `O(1)`.

Total:

```text id="ct013"
O(n)
```

#### 7. Postorder + Inorder — Good to Know

Postorder:

```text id="ct014"
Left → Right → Root
```

Therefore:

1. Last postorder value → Root.
2. Inorder still separates left/right subtrees.
3. When processing postorder **backwards**, construct:

```text id="ct015"
Right subtree first
Left subtree second
```

This is the main difference from preorder construction.

#### 8. Important Limitation — Must Know

Traversal combinations matter.

```text id="ct016"
Preorder + Inorder   → Unique tree
Postorder + Inorder  → Unique tree

Preorder alone       → Not generally unique
Postorder alone      → Not generally unique
```

This assumes node values are **unique**, which is the standard form of this interview problem.

#### 9. Complexity & Key Points — Must Know

1. Time → `O(n)` with an inorder index HashMap.
2. Space → `O(n)` for HashMap + recursion.
3. Preorder → **root first**.
4. Postorder → **root last**.
5. Inorder → separates **left and right subtrees**.
6. Preorder + Inorder → construct **left before right**.
7. Reverse Postorder + Inorder → construct **right before left**.
8. Avoid repeatedly scanning inorder; use a **HashMap** for `O(1)` index lookup.