---
title: "The Myers Difference Algorithm"
date: 2025-09-11
tags: ["algorithm"]
---

I came across this algorithm when trying to solve a real-world problem.

I am working on a MS Word add-in that can modify the document. Previously, I directly called the replaceSelection function call, but this can lead to a poor result because what people want is to quickly locate where the difference is; let me explain.

original: "This Agreement shall commence on [Start Date] and shall continue until terminated by either party. Employment is at-will and may be terminated by either party with or without cause, with two (2) weeks written notice."  
new: "This Agreement shall commence on [Start Date] and shall continue until terminated by either party. Employment is at-will and may be terminated by either party with or without cause, with four (4) weeks written notice."

Previously, the whole original paragraph will be marked as a single deletion and the new paragraph will be marked as a single addition. This is problematic because, it will take a reviewer quite a while to find out what exactly have changed throughout this paragraph; and when they discovered that it's only a number change, they would want this add-in to find a better way to diff it, i.e., smallest possible number of changes to the original in order to produce the new result.

Introducing the Myers difference algorithm feat. longest common sequence.

todo:

https://blog.jcoglan.com/2017/02/12/the-myers-diff-algorithm-part-1/

https://www.nathaniel.ai/myers-diff/

https://stackoverflow.blog/2024/12/20/this-developer-tool-is-40-years-old-can-it-be-improved/