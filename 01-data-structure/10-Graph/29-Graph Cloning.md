# Graph Cloning

#### 1. Definition — Must Know

1. **Graph Cloning** means creating a **deep copy** of a graph.
2. Every original node gets a new cloned node.
3. All connections between nodes must be recreated using the **cloned nodes**.
4. The cloned graph must not reference original nodes.

```text id="gc01"
Original Graph        Cloned Graph

1 --- 2               1' --- 2'
|     |               |      |
4 --- 3               4' --- 3'
```

#### 2. Why It Is Tricky — Must Know

Graphs can contain:

```text id="gc02"
Cycles
Shared Neighbors
Multiple Paths
```

Example:

```text id="gc03"
1 → 2 → 3
↑       |
└───────┘
```

Without tracking already-cloned nodes, recursion can continue forever or create duplicate clones.

Therefore we need:

```text id="gc04"
Original Node → Cloned Node
```

Usually:

```text id="gc05"
HashMap<Node, Node>
```

#### 3. Core Pattern — Must Know

The most important idea:

```text id="gc06"
Map<Original, Clone>
```

The map does two jobs:

1. Acts like `visited`.
2. Stores the corresponding cloned node.

Example:

```text id="gc07"
Original     Clone

Node 1   →   Node 1'
Node 2   →   Node 2'
Node 3   →   Node 3'
```

#### 4. Node Structure

Typical graph node:

```kotlin id="gc08"
class Node(
    val value: Int
) {
    val neighbors = mutableListOf<Node>()
}
```

#### 5. DFS Logic — Must Know

```text id="gc09"
clone(node):

1. If node already exists in map:
      return existing clone

2. Create clone of current node.

3. Store it in map immediately.

4. Visit every neighbor.

5. Clone each neighbor recursively.

6. Add cloned neighbors to cloned node.

7. Return cloned node.
```

Important:

```text id="gc10"
Create Clone
     ↓
Store in Map
     ↓
Clone Neighbors
```

Store the clone **before** exploring neighbors because the graph may contain cycles.

#### 6. Kotlin DFS Implementation — Must Know

```kotlin id="gc11"
fun cloneGraph(node: Node?): Node? {

    if (node == null) {
        return null
    }

    val clones = HashMap<Node, Node>()

    fun dfs(current: Node): Node {

        if (clones.containsKey(current)) {
            return clones[current]!!
        }

        val clone = Node(current.value)

        clones[current] = clone

        for (neighbor in current.neighbors) {

            clone.neighbors.add(
                dfs(neighbor)
            )
        }

        return clone
    }

    return dfs(node)
}
```

#### 7. Why Store Before DFS? — Must Know

Suppose:

```text id="gc12"
1 --- 2
|     |
└─────┘
```

During:

```text id="gc13"
clone(1)
   ↓
clone(2)
   ↓
clone(1)
```

If `1` was not already stored in the map:

```text id="gc14"
1 → 2 → 1 → 2 → ...
```

Infinite recursion.

Correct:

```text id="gc15"
Create clone(1)
Store clone(1)
Then explore node 2
```

#### 8. BFS Approach — Good to Know

Graph cloning can also use BFS.

Core logic:

```text id="gc16"
1. Create clone of start node.

2. Store original → clone in map.

3. Add original node to Queue.

4. For every neighbor:

   if neighbor not cloned:
       create clone
       store in map
       add original neighbor to Queue

5. Connect current clone to neighbor clone.
```

#### 9. Kotlin BFS Implementation

```kotlin id="gc17"
fun cloneGraph(node: Node?): Node? {

    if (node == null) {
        return null
    }

    val clones = HashMap<Node, Node>()
    val queue = ArrayDeque<Node>()

    clones[node] = Node(node.value)
    queue.addLast(node)

    while (queue.isNotEmpty()) {

        val current = queue.removeFirst()

        for (neighbor in current.neighbors) {

            if (!clones.containsKey(neighbor)) {

                clones[neighbor] = Node(neighbor.value)
                queue.addLast(neighbor)
            }

            clones[current]!!.neighbors.add(
                clones[neighbor]!!
            )
        }
    }

    return clones[node]
}
```

#### 10. Time & Space Complexity — Must Know

Every node is cloned once and every edge is processed.

```text id="gc18"
Time → O(V + E)
```

Map stores up to `V` nodes.

DFS recursion / BFS queue:

```text id="gc19"
Extra Space → O(V)
```

The cloned graph itself requires:

```text id="gc20"
O(V + E)
```

#### 11. Shallow Copy vs Deep Copy — Must Know

Wrong:

```text id="gc21"
Clone Node
   ↓
Reuse original neighbors
```

That is not a proper graph clone.

Correct:

```text id="gc22"
Original Node → New Node

Original Neighbor → New Neighbor
```

Every node must be newly created.

#### 12. DFS vs BFS

```text id="gc23"
DFS                         BFS

Recursion / Stack           Queue

Simple implementation       Avoids deep recursion

Map required                Map required

O(V + E)                    O(V + E)
```

For interviews:

```text id="gc24"
DFS + HashMap
```

is usually the simplest approach.

#### 13. Common Interview Patterns — Must Know

Graph cloning mainly tests whether you understand:

1. Graph traversal.
2. Cycles.
3. Deep copy.
4. HashMap mapping.
5. DFS/BFS.
6. Shared references.

Core pattern:

```text id="gc25"
Traversal
+
Original → Clone Map
```

#### 14. Common Edge Cases — Must Know

1. `node == null`.
2. Single node.
3. Self-loop.
4. Cyclic graph.
5. Multiple nodes sharing the same neighbor.
6. Duplicate connections if allowed by the input.

Self-loop:

```text id="gc26"
A ──┐
↑   |
└───┘
```

The cloned node must point to **itself**, not the original node.

#### 15. Common Mistakes — Must Know

1. Creating multiple clones for the same node.
2. Not using a HashMap.
3. Storing the clone only after processing neighbors.
4. Infinite recursion because of cycles.
5. Connecting cloned nodes to original neighbors.
6. Using node value as the map key when values are not guaranteed unique.

Prefer:

```kotlin id="gc27"
HashMap<Node, Node>()
```

instead of:

```kotlin id="gc28"
HashMap<Int, Node>()
```

unless node values are guaranteed unique.

#### 16. Interview Must Remember

1. Graph Cloning = **deep copy of a graph**.
2. Use **DFS or BFS**.
3. Maintain:

```text id="gc29"
Original Node → Cloned Node
```

4. HashMap also acts as `visited`.
5. **Store clone before exploring neighbors**.
6. Never connect cloned nodes to original nodes.
7. Complexity → **`O(V + E)`**.
8. Core interview pattern → **Graph Traversal + HashMap**.