---
title: "Union Find (Disjoint Set Union)"
date: 2025-07-14
tags: ["algorithm", "neetcode150", "union-find", "python"]
---

Time to master union find to end this all.

Union Find, also known as Disjoint Set Union (DSU), is a data structure that keeps track of a partition of a set into disjoint (non-overlapping) subsets. It provides two primary operations: `find` and `union`. The `find` operation determines the root representative of the set containing a particular element, while the `union` operation merges two sets into a single set. This structure is particularly useful in scenarios where we need to determine the connected components of a graph, such as in Kruskal's algorithm for finding the Minimum Spanning Tree or in solving the Longest Consecutive Sequence problem efficiently. The efficiency of Union Find can be significantly improved with techniques like path compression and union by rank, which help in keeping the tree flat and operations nearly constant time.

It's a versatile and useful structure to tackle quite a range of problems, and the interviewer can expect you to have it in your toolbox.

### naive implementation for Union Find

```python
class DSU:  # Disjoint Set Union
    def __init__(self, size):
        # init parent array with each element as its own parent
        self.parent = list(range(size))
    
    def find(self, i):
        if self.parent[i] == i:
            return i
        
        return self.find(self.parent[i])

    def union(self, i, j):
        i_parent = self.find(i)
        j_parent = self.find(j)

        self.parent[i_parent] = j_parent
```

Straightforward but not enough for tech rounds.

### Path Compression in find()

```python
    def find(self, i):
        # if I am the root of all connected
        if self.parent[i] == i:
            return i

        # if I am not the root of all connected
        self.parent[i] = self.find(self.parent[i])  # find the root using my parent and make it my parent (compression), also recursively sets common root to all my parents
        return self.parent[i]
```

This assignment keeps all children directly pointing at a single root (rather than the naive method, which can be a linked list-like structure than a tree in worst case scenarios), thus compressing the height of the trees.

### Union by Rank

We want to further optimize when performing union(). We need to decide whether to join A to B, or B to A, in order to minimize the height of the union'ed tree.

If A is shallow and B is deep (taller in height), we would want to join A into B rather than the opposite. Let me explain:

For example, if you have a tree A of height 3 and tree B of height 5, you will want to join A into B since it will make the overall maximum height still 5 (i.e., you are chaining a 3 (everything in A) after 1 (the root in B), which gets you 4 (the root in B, with everything in A), which is shallower than 5 (B's height), which prevented your maximum height from growing).  
If you do it the opposite way, the maximum height will now be `max(3, 5+1)` = 6.

If both have equal height, it is inevitable (either way) to have our maximum height += 1.

Rank does not necessarily equal to height. Rank is only an approximation:

<details><summary>Our current setup does not support an accurate height tracker, why?</summary>
    <details><summary>Because we didn't do any updates to height during path compression, which we should, we could, but we needn't for DSU, why?</summary>
        As long as we keep track of a "height" that is accurate in a relative way (i.e., given rank >= height, rank A >= rank B can be reliably translated into height A >= height B), this is all we need.
    </details>
</details>

```python
    def __init__(self, n):
        self.rank = [0] * n  # we need another list to keep rough track of heights
        self.parent = list(range(n))

    # def find() omitted

    def union(self, i, j):
        i_parent = self.find(i)
        j_parent = self.find(j)

        if i_parent == j_parent:
            return
        
        # if tree i is shallower than j
        if self.rank[i_parent] < self.rank[j_parent]:
            # join tree i into j
            self.parent[i_parent] = j_parent
        elif self.rank[i_parent] > self.rank[j_parent]:
            self.parent[j_parent] = i_parent
        # if tree i and j have the same height
        else:
            # either works, but you need to increment rank for the chosen parent - "Uneasy lies the head that wears a crown."
            self.parent[j_parent] = i_parent
            self.rank[i_parent] += 1
```

---

### optimized implementation

```python
class DSU:
    def __init__(self, n):
        self.rank = [0] * n
        self.parent = list(range(n))
    
    def find(self, i):
        if self.parent[i] != i:
            self.parent[i] = self.find(self.parent[i])

        return self.parent[i]

    
    def union(self, i, j):
        i_parent = self.find(i)
        j_parent = self.find(j)

        if i_parent == j_parent:
            return
        
        i_parent_rank = self.rank[i_parent]
        j_parent_rank = self.rank[j_parent]

        if i_parent_rank < j_parent_rank:
            self.parent[i_parent] = j_parent
        elif i_parent_rank > j_parent_rank:
            self.parent[j_parent] = i_parent
        else:
            self.parent[j_parent] = i_parent
            self.rank[i_parent] += 1
```

Time Complexity:
- find: O(α(n)) ≈ O(1) (amortized)
- union: O(α(n)) ≈ O(1) (amortized)
- Overall: O(α(n)) ≈ O(1) (amortized) per operation

I might expand on α(n), the inverse Ackermann function some day.