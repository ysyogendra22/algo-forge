# Validate BST

#### 1. Definition — Must Know

1. **Validate BST** checks whether a Binary Tree satisfies Binary Search Tree rules.
2. For every node:
   - All values in left subtree `< node`
   - All values in right subtree `> node`
3. The rule must hold for the **entire subtree**, not only immediate children.

#### 2. Why It Is Important — Must Know

A common mistake is checking only:

```text id="qj81mb"
node.left < node < node.right
```

That is **not enough**.

Example:

```text id="3pk2de"
        10
       /  \
      5    15
          /  \
         6    20
```

`6 < 15` looks correct locally, but `6` is in the right subtree of `10`.

Since:

```text id="7h5f0m"
6 < 10
```

the tree is **not a valid BST**.

#### 3. Correct Logic — Range / Bounds — Must Know

Pass an allowed range to every node:

```text id="9em42k"
Root        → (-∞, +∞)

Left child  → (min, root)
Right child → (root, max)
```

For every node:

```text id="1d6cl3"
min < node.value < max
```

Then recursively update the boundaries.

#### 4. Kotlin Implementation — Must Know

```kotlin id="93w2fc"
fun isValidBST(root: TreeNode?): Boolean {
    return validate(root, Long.MIN_VALUE, Long.MAX_VALUE)
}

fun validate(
    node: TreeNode?,
    min: Long,
    max: Long
): Boolean {
    if (node == null) return true

    if (node.value <= min || node.value >= max) {
        return false
    }

    return validate(node.left, min, node.value.toLong()) &&
           validate(node.right, node.value.toLong(), max)
}
```

#### 5. How It Works

For:

```text id="a8y91z"
        10
       /  \
      5    15
          /  \
         12   20
```

Ranges become:

```text id="v3k5dq"
10 → (-∞, +∞)

5  → (-∞, 10)

15 → (10, +∞)

12 → (10, 15)

20 → (15, +∞)
```

Every node must stay inside its allowed range.

#### 6. Alternative: Inorder Traversal — Good to Know

Inorder traversal of a valid BST must be **strictly increasing**.

```text id="m7hd4a"
Left → Root → Right

2 → 5 → 8 → 10 → 15
```

If:

```text id="7ycs1n"
current <= previous
```

the tree is invalid.

Range validation is usually the cleaner approach in interviews.

#### 7. Complexity & Key Points — Must Know

1. Time → `O(n)` because every node may need to be checked.
2. Space → `O(h)` for recursion.
3. Balanced tree → `O(log n)` recursion space.
4. Skewed tree → `O(n)` recursion space.
5. Never validate only immediate `left` and `right` children.
6. Think in terms of **allowed range/boundaries**.
7. Use `Long.MIN_VALUE` / `Long.MAX_VALUE` to safely handle `Int` boundary values.
8. Duplicate values are invalid when using the standard strict BST rule: `Left < Root < Right`.