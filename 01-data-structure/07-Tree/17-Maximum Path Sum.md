# Maximum Path Sum

#### 1. Definition — Must Know

1. **Maximum Path Sum** is the largest sum obtainable from any valid path in a Binary Tree.
2. A path can start and end at **any nodes**.
3. Each connected node can appear only once in the path.
4. The path does **not** need to pass through the root.

#### 2. How It Works — Must Know

```text id="mps001"
       -10
       /  \
      9    20
          /  \
         15   7
```

Best path:

```text id="mps002"
15 → 20 → 7
```

Sum:

```text id="mps003"
15 + 20 + 7 = 42
```

Answer → `42`

#### 3. Core Idea — Must Know

At every node calculate two different things:

```text id="mps004"
1. Path through current node
   = node + leftGain + rightGain

2. Path returned to parent
   = node + max(leftGain, rightGain)
```

Why?

A path going **up to the parent cannot take both branches**.

```text id="mps005"
        Parent
          |
         Node
        /    \
      Left   Right

Return upward → choose Left OR Right

Final answer at Node → can use Left + Node + Right
```

This distinction is the key to the problem.

#### 4. Core Logic — Must Know

Use **bottom-up DFS / Postorder**.

```text id="mps006"
1. Get maximum gain from left subtree.
2. Get maximum gain from right subtree.
3. Ignore negative gains.
4. Calculate path through current node.
5. Update global maximum.
6. Return the best one-branch path to parent.
```

Formula:

```text id="mps007"
left  = max(0, dfs(left))
right = max(0, dfs(right))

currentPath = node.value + left + right

answer = max(answer, currentPath)

return node.value + max(left, right)
```

#### 5. Kotlin Implementation — Must Know

```kotlin id="mps008"
fun maxPathSum(root: TreeNode?): Int {
    var maxSum = Int.MIN_VALUE

    fun dfs(node: TreeNode?): Int {
        if (node == null) return 0

        val left = maxOf(0, dfs(node.left))
        val right = maxOf(0, dfs(node.right))

        val currentPath = node.value + left + right

        maxSum = maxOf(maxSum, currentPath)

        return node.value + maxOf(left, right)
    }

    dfs(root)

    return maxSum
}
```

#### 6. Why Ignore Negative Paths? — Must Know

Example:

```text id="mps009"
       10
      /  \
    -20   5
```

Including `-20` makes the path worse.

Therefore:

```text id="mps010"
max(0, subtreeGain)
```

means:

```text id="mps011"
Negative contribution → Don't use it
```

#### 7. Important Edge Case — Must Know

All values can be negative:

```text id="mps012"
       -10
       / \
     -20 -3
```

Answer:

```text id="mps013"
-3
```

This is why:

```kotlin id="mps014"
var maxSum = Int.MIN_VALUE
```

is important.

Initializing it to `0` would incorrectly return `0`.

#### 8. Connection to Diameter — Must Know

The pattern is very similar to **Diameter of Binary Tree**.

```text id="mps015"
Diameter:
Track  → leftHeight + rightHeight
Return → 1 + max(leftHeight, rightHeight)

Maximum Path Sum:
Track  → node + leftGain + rightGain
Return → node + max(leftGain, rightGain)
```

Both use **bottom-up DFS**.

#### 9. Complexity & Key Points — Must Know

1. Time → `O(n)` — every node is processed once.
2. Space → `O(h)` — recursion stack.
3. Balanced tree → `O(log n)` stack space.
4. Skewed tree → `O(n)` stack space.
5. Path can start/end at **any node**.
6. Global answer can use **both branches**.
7. Value returned to parent can use only **one branch**.
8. Ignore negative subtree gains using `maxOf(0, gain)`.
9. Initialize global maximum with `Int.MIN_VALUE`.
10. Recognize this as a classic **bottom-up DFS + global maximum** pattern.