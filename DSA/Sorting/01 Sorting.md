### Sorting

**Sorting** is the process of rearranging elements according to a defined ordering criterion, typically ascending or descending.

Example : Sorting isn't limited to numbers. You can sort:
Numbers   → by value
Strings   → alphabetically
Users     → by name, age, salary
Products  → by price, rating
Logs      → by timestamp

### Why sorting is useful: 
Sorting organizes data so that searching, comparison, merging, duplicate detection, and many other operations can be performed more efficiently.


### Types : 
### 🔴 Must Know
1. Bubble Sort
2. Selection Sort
3. Insertion Sort
4. Merge Sort
5. Quick Sort
6. Heap Sort

### 🟡 Good to Know
7. Counting Sort
8. Radix Sort
9. Bucket Sort

### ⚪ Awareness Only
10. Tim Sort
11. Shell Sort
12. Cycle Sort
13. Comb Sort
14. Pigeonhole Sort
15. External Sort


### Stable/Unstable Sorting

> **Stable sort preserves the relative order of equal elements; unstable sort does not guarantee it.**

**Easy memory trick:**  
**Stable = Equal items stay in the same order.**


### Stable Sorting

If two elements have the same key, their **original relative order is preserved**.

```
Before:
(A, 20), (B, 10), (C, 20)

Sort by number:

(B, 10), (A, 20), (C, 20)
          ↑        ↑
          A stays before C
```

A and C both have `20`. Since A was before C originally, it remains before C.

### Unstable Sorting

Elements with the same key **may change their relative order**.

```
Before:
(A, 20), (B, 10), (C, 20)

Possible result:

(B, 10), (C, 20), (A, 20)
          ↑        ↑
          order changed
```

#### Stable Sorting
- Bubble Sort
- Insertion Sort
- Merge Sort
- Counting Sort
- Radix Sort
- Tim Sort

#### Unstable Sorting
- Selection Sort
- Quick Sort
- Heap Sort
- Shell Sort
- Cycle Sort
- Comb Sort