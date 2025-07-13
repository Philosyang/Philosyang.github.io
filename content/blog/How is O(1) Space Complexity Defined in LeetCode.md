---
title: "How is O(1) Space Complexity Defined in LeetCode"
date: 2025-07-12
tags: ["algorithm", "python"]
---

"""  
When we talk about space complexity in algorithm analysis, we usually focus on auxiliary (extra) space, not including the output space.  
When we talk about space complexity, we mean the additional space used beyond the input and output.  
Output space is not counted because it's required and unavoidable.  
"""  
is what I get from language models. But this is inconsistent with what we typically reach for in LeetCode. For example:  
```python
def square_nums_1(nums):
    return [x*x for x in nums]
```
```python
def square_nums_2(nums):
    for i in range(len(nums)):
        nums[i] *= nums[i]
    return nums
```

Output space are both O(n), it is unavoidable.  
However, we would _classify_ the first method as O(n), while the second method as O(1) since it is in-place.

---

To my understandings, the key is what the problem allows/requires.  
If the problem allows / is fine with modifying the input, the above examples' space complexity will be O(n) and O(1); since whether or not creating a new array is an algorithm choice by us.  
If the problem asked for a new array, then the new array is a required output, which will not be counted as auxiliary space.  
The distinction only matters when we have a choice between modifying input vs. creating new output.

Therefore, [238.](https://leetcode.com/problems/product-of-array-except-self/description/)'s O(1) follow-up is _considered_ as O(1) because the problem asked to "return an array `answer`", i.e., the `answer` array of length n is a required output.

---

Let me know if you have an even better definition of "O(1) vs. O(n) space complexity in LeetCode".