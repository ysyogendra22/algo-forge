# Serialize / Deserialize Tree

#### 1. Definition — Must Know

1. **Serialize** → Convert a tree into a string/sequence.
2. **Deserialize** → Reconstruct the original tree from that representation.
3. The serialized data must preserve both **node values and tree structure**.

#### 2. Why It Is Used — Must Know

1. Store a tree in a file/database.
2. Send a tree across a network.
3. Reconstruct the exact same tree later.
4. Common interview problem for testing **DFS + tree reconstruction**.

#### 3. How It Works — Must Know

Tree:

```text id="sd001"
        1
       / \
      2   3
         / \
        4   5
```

Using **Preorder DFS**:

```text id="sd002"
Root → Left → Right
```

Serialized:

```text id="sd003"
1,2,#,#,3,4,#,#,5,#,#
```

`#` represents a `null` child.

Without null markers, the exact tree structure may be lost.

#### 4. Core Logic — Must Know

Serialize:

```text id="sd004"
1. Visit current node.
2. Store its value.
3. Serialize left subtree.
4. Serialize right subtree.
5. Store "#" when node is null.
```

Deserialize:

```text id="sd005"
1. Read next value.
2. "#" → return null.
3. Otherwise create node.
4. Build its left subtree.
5. Build its right subtree.
6. Return node.
```

The deserialize order must match the serialize order.

#### 5. Serialize — Kotlin — Must Know

```kotlin id="sd006"
fun serialize(root: TreeNode?): String {
    val result = mutableListOf<String>()

    fun dfs(node: TreeNode?) {
        if (node == null) {
            result.add("#")
            return
        }

        result.add(node.value.toString())

        dfs(node.left)
        dfs(node.right)
    }

    dfs(root)

    return result.joinToString(",")
}
```

#### 6. Deserialize — Kotlin — Must Know

```kotlin id="sd007"
fun deserialize(data: String): TreeNode? {
    val values = data.split(",")
    var index = 0

    fun dfs(): TreeNode? {
        if (values[index] == "#") {
            index++
            return null
        }

        val node = TreeNode(values[index].toInt())
        index++

        node.left = dfs()
        node.right = dfs()

        return node
    }

    return dfs()
}
```

#### 7. Why Null Markers Matter — Must Know

Consider:

```text id="sd008"
    1
   /
  2
```

and:

```text id="sd009"
1
 \
  2
```

Without `null` markers, both could become:

```text id="sd010"
1,2
```

With markers:

```text id="sd011"
Left child  → 1,2,#,#,#

Right child → 1,#,2,#,#
```

Now the structures are distinguishable.

#### 8. BFS Approach — Good to Know

Serialization can also use **Level Order / BFS**.

Example:

```text id="sd012"
1,2,3,#,#,4,5,#,#,#,#
```

1. DFS preorder is usually simpler to implement recursively.
2. BFS is also valid if null positions are preserved.
3. You only need to be comfortable with one solid approach in an interview unless specifically asked otherwise.

#### 9. Complexity & Key Points — Must Know

1. Serialize time → `O(n)`.
2. Deserialize time → `O(n)`.
3. Serialized output space → `O(n)`.
4. DFS recursion space → `O(h)`.
5. Serialization must preserve **values + structure**.
6. Use explicit markers such as `#` for `null`.
7. Serialize and deserialize must follow the **same traversal format**.
8. Preorder DFS is one of the simplest approaches: `Root → Left → Right`.
9. Don't serialize only node values; different tree shapes can contain the same traversal values.