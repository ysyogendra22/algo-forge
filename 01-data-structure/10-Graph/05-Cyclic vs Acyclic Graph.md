# Cyclic vs Acyclic Graph

#### 1. Definition — Must Know

1. **Cyclic Graph** → Contains at least one cycle.
2. **Acyclic Graph** → Contains no cycle.
3. A **cycle** is a path that starts and returns to the same vertex without reusing edges in the cycle.

#### 2. How It Works — Must Know

Cyclic:

```text
A → B
↑   ↓
└── C
```

Path:

```text
A → B → C → A
```

returns to `A`, so a cycle exists.

Acyclic:

```text
A → B → C
    ↓
    D
```

There is no path that loops back to its starting vertex.

#### 3. Directed vs Undirected Cycles — Must Know

**Undirected Graph**

```text
A ----- B
|       |
C ----- D
```

A cycle exists:

```text
A → B → D → C → A
```

**Directed Graph**

```text
A → B → C
    ↑   ↓
    └── D
```

A cycle exists only when the **edge directions** allow returning to an earlier node:

```text
B → C → D → B
```

#### 4. DAG — Must Know

**DAG = Directed Acyclic Graph**

```text
A → B → D
 \  ↓
  → C
```

1. Directed edges.
2. No cycles.
3. Commonly represents dependencies.

Examples:

1. Task dependencies.
2. Course prerequisites.
3. Build systems.
4. Workflow dependencies.

DAGs are strongly associated with **Topological Sort**.

#### 5. Cycle Detection — Must Know Concept

For an **Undirected Graph**:

```text
DFS/BFS + Visited + Parent
```

1. Visit a node.
2. Track which node you came from.
3. If you reach an already visited neighbor that is **not the parent** → cycle exists.

For a **Directed Graph**:

```text
DFS + Current Recursion Path
```

1. Track visited nodes.
2. Track nodes currently in the DFS path.
3. If an edge reaches a node already in the current path → cycle exists.

Implement these separately when studying **Cycle Detection**.

#### 6. Why Cycles Matter — Must Know

1. Dependency cycle can make execution order impossible.
2. Cycles affect traversal because you can revisit nodes indefinitely without a `visited` mechanism.
3. Detecting cycles is important for dependency and scheduling problems.
4. A directed graph can have a topological ordering **only if it is acyclic**.

#### 7. Key Points — Must Know

1. Cyclic → contains at least one cycle.
2. Acyclic → contains no cycles.
3. **DAG** → Directed + Acyclic.
4. Cycle detection differs between **directed and undirected graphs**.
5. Graph traversal usually needs a `visited` structure to prevent repeated processing.
6. **DAG + dependency ordering → think Topological Sort**.
7. **Cycle detection → think DFS/BFS state tracking**, depending on graph type.