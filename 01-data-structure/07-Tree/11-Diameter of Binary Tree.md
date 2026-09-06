# Diameter of Binary Tree

#### 1. Definition — Must Know

1. **Diameter** is the length of the longest path between any two nodes in a Binary Tree.
2. The path **does not need to pass through the root**.
3. Diameter is commonly measured by the **number of edges**.

#### 2. How It Works — Must Know

```text id="d9t3k2"
        1
       / \
      2   3
     / \
    4   5
```

Longest path:

```text id="v4km3p"
4 → 2 → 1 → 3
```

Diameter:

```text id="n2q7hb"
3 edges
```

At each node:

```text id="w7kr4m"
diameter through node = leftHeight + rightHeight
```

#### 3. Core Logic — Must Know

Use **bottom-up DFS / Postorder**.

```text id="g3fn9q"
1. Calculate left subtree height.
2. Calculate right subtree height.
3. Calculate:
   diameter = leftHeight + rightHeight
4. Update maximum diameter.
5. Return:
   1 + max(leftHeight, rightHeight)
```

Important distinction:

```text id="k9r2vc"
Height   → longest downward path from current node.

Diameter → longest path between any two nodes.
```

#### 4. Kotlin Implementation — Must Know

```kotlin id="t6pz2n"
fun diameterOfBinaryTree(root: TreeNode?): Int {
    var diameter = 0

    fun height(node: TreeNode?): Int {
        if (node == null) return 0

        val left = height(node.left)
        val right = height(node.right)

        diameter = maxOf(diameter, left + right)

        return 1 + maxOf(left, right)
    }

    height(root)

    return diameter
}
```

#### 5. Why `left + right`? — Must Know

```text id="p8dv5j"
          Node
         /    \
        /      \
 deepest      deepest
 left          right
```

The longest path passing through the current node combines:

```text id="x4tm8c"
Left path + Right path
```

So:

```text id="s7qn3m"
candidate diameter = leftHeight + rightHeight
```

#### 6. Common Pattern — Must Know

This is a classic **bottom-up DFS** pattern:

```text id="q6kh4w"
Return one value → Height

Track another value → Maximum Diameter
```

The same idea appears in problems such as:

1. Maximum Path Sum.
2. Longest path problems.
3. Subtree calculations.

#### 7. Complexity & Key Points — Must Know

1. Time → `O(n)` — every node is processed once.
2. Space → `O(h)` — recursion stack.
3. Balanced tree stack → `O(log n)`.
4. Skewed tree stack → `O(n)`.
5. Diameter does **not** have to pass through the root.
6. At each node → `leftHeight + rightHeight`.
7. Return height → `1 + max(left, right)`.
8. Avoid recalculating height separately for every node; that can make the solution `O(n²)`.