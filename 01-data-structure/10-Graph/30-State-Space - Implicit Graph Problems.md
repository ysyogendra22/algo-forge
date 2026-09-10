# State-Space / Implicit Graph Problems

#### 1. Definition — Must Know

1. An **Implicit Graph** is a graph where nodes and edges are **not explicitly given**.
2. You generate neighbors from the current **state** using the problem's allowed operations.
3. Each state acts like a graph node.
4. Each valid transition acts like an edge.

```text id="ig01"
State      → Vertex
Operation  → Edge
```

#### 2. Why It Is Important — Must Know

Many interview problems do not look like graph problems.

Example:

```text id="ig02"
Start = "0000"
Target = "0202"

Operation:
Turn one digit +1 or -1
```

No graph is provided.

But:

```text id="ig03"
"0000" → Node

"0001", "0009", "0010"... → Neighbors

One operation → Edge
```

So it is an **implicit graph**.

#### 3. Explicit vs Implicit Graph

```text id="ig04"
Explicit Graph                Implicit Graph

Adjacency list given          Neighbors generated

Nodes provided                States represent nodes

Edges provided                Operations represent edges

graph[node]                   generateNeighbors(state)
```

Important:

```text id="ig05"
Do NOT build the entire graph
if neighbors can be generated when needed.
```

#### 4. How to Recognize It — Must Know

Look for phrases like:

```text id="ig06"
Minimum moves
Minimum steps
Minimum transformations
Reach target
Change one thing at a time
Allowed operations
Possible states
```

Then think:

```text id="ig07"
Can I model each situation as a state
and each operation as an edge?
```

If yes → graph traversal may apply.

#### 5. Core Modeling — Must Know

Every state-space problem needs three things:

```text id="ig08"
1. State
2. Transition
3. Goal
```

Example:

```text id="ig09"
Word Ladder

State      → Current word
Transition → Change one character
Goal       → Target word
```

Another example:

```text id="ig10"
Grid

State      → (row, column)
Transition → Move up/down/left/right
Goal       → Destination
```

#### 6. BFS Pattern — Must Know

If every transition has the **same cost** and the question asks:

```text id="ig11"
Minimum moves / steps / transformations
```

use:

```text id="ig12"
BFS
```

Why?

```text id="ig13"
Level 0 → 0 moves
Level 1 → 1 move
Level 2 → 2 moves
Level 3 → 3 moves
```

The first time the target is reached gives the minimum number of transitions.

#### 7. Generic BFS Template — Must Know

```kotlin id="ig14"
fun shortestSteps(start: String, target: String): Int {

    val queue = ArrayDeque<Pair<String, Int>>()
    val visited = mutableSetOf<String>()

    queue.addLast(start to 0)
    visited.add(start)

    while (queue.isNotEmpty()) {

        val (state, steps) = queue.removeFirst()

        if (state == target) {
            return steps
        }

        for (next in generateNeighbors(state)) {

            if (visited.add(next)) {
                queue.addLast(next to steps + 1)
            }
        }
    }

    return -1
}
```

Core structure:

```text id="ig15"
Start
  ↓
BFS
  ↓
Generate Neighbors
  ↓
Visited Check
  ↓
Target?
```

#### 8. Visited Is Critical — Must Know

State transitions can create cycles.

Example:

```text id="ig16"
A → B
B → A
```

Without visited:

```text id="ig17"
A → B → A → B → A ...
```

So maintain:

```kotlin id="ig18"
val visited = mutableSetOf<State>()
```

Mark a state visited when adding it to the queue.

#### 9. State Representation — Must Know

Choosing the right state is often the hardest part.

Simple state:

```text id="ig19"
Current Word
Current Number
Current Position
```

Complex state:

```text id="ig20"
(row, col, keysCollected)

(node, remainingStops)

(position, usedMask)
```

Rule:

```text id="ig21"
State must contain all information
needed to make future decisions.
```

If two situations have different future possibilities, they may need to be treated as different states.

#### 10. Common Example — Word Ladder

```text id="ig22"
hit → hot → dot → dog → cog
```

Model:

```text id="ig23"
Vertex → Word

Edge → Two words differ by one valid character change
```

Question:

```text id="ig24"
Minimum transformations?
```

Use:

```text id="ig25"
BFS
```

You usually generate valid neighboring words dynamically rather than building the complete graph first.

#### 11. Common Example — Open the Lock

State:

```text id="ig26"
"0000"
```

Operations:

```text id="ig27"
Turn any wheel:

+1
or
-1
```

Each generated combination is a neighboring state.

```text id="ig28"
"0000"
  ↓
"1000"
"9000"
"0100"
"0900"
...
```

Minimum turns:

```text id="ig29"
BFS
```

#### 12. BFS vs DFS vs Dijkstra — Must Know

```text id="ig30"
Need any valid solution
        ↓
      DFS/BFS


Minimum moves
All transitions equal cost
        ↓
       BFS


Different non-negative transition costs
        ↓
     Dijkstra


Explore all combinations / backtrack
        ↓
       DFS
```

Algorithm depends on the **edge/transition cost**, not whether the graph is explicit.

#### 13. Multi-Source State-Space — Good to Know

If multiple states are valid starting points:

```text id="ig31"
S1
S2
S3
```

Initialize:

```text id="ig32"
Queue = [S1, S2, S3]
```

Then run:

```text id="ig33"
Multi-Source BFS
```

Useful for nearest-source or spreading problems.

#### 14. Complexity — Must Know

Implicit graph complexity still follows:

```text id="ig34"
O(V + E)
```

But here:

```text id="ig35"
V = Number of reachable states

E = Number of valid transitions
```

If every state generates at most `K` neighbors:

```text id="ig36"
Time ≈ O(Number of States × K)
```

Space:

```text id="ig37"
O(Number of States)
```

for queue + visited in the worst case.

The state space can sometimes be very large, so avoid generating unnecessary states.

#### 15. Common Interview Patterns — Must Know

1. **Word transformations**
   ```text
   Word Ladder
   ```

2. **Minimum operations**
   ```text
   Number/state transformations
   ```

3. **Lock combinations**
   ```text
   Open the Lock
   ```

4. **Board movement**
   ```text
   Position = State
   ```

5. **Minimum moves in games**
   ```text
   BFS
   ```

6. **States with extra conditions**
   ```text
   (position, additionalState)
   ```

#### 16. Common Mistakes — Must Know

1. Not recognizing the problem as a graph.
2. Building the complete graph unnecessarily.
3. Using DFS for minimum moves with equal-cost transitions.
4. Forgetting `visited`.
5. Marking visited too late.
6. Using an incomplete state representation.
7. Generating invalid neighbors.
8. Forgetting blocked/forbidden states.
9. Assuming `O(V + E)` is small without considering how large the state space can become.

#### 17. Interview Must Remember

1. **State = Vertex**.
2. **Valid operation = Edge**.
3. Generate neighbors **on demand**.
4. Minimum equal-cost moves → **BFS**.
5. Different non-negative costs → **Dijkstra**.
6. Use `visited` to avoid repeated states/cycles.
7. State must contain **everything needed for future decisions**.
8. When a problem says **minimum moves/transformations**, check whether it is an **implicit graph**.