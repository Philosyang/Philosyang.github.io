---
title: "Python set.remove() - O(1) or O(n)?"
date: 2025-10-25
tags: ["algorithm", "python"]
---

In practice, the amortized complexity for set.remove() should be O(1), since each element is hashed with a hash function. However, the worst-case scenario will involve hash collisions / bad hash distributions (lots of different elements ending in the same hash bucket) that requires scanning through multiple elements to find x.

On the other hand, when we say "Big O", we mean the worst-case time complexity.

set.remove() is indeed O(n) in theoretical Big O (worst case), but O(1) amortized / on average. In practical python performance discussions, I would say it's O(1) because the average case dominates in real-world use.