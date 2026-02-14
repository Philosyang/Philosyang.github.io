---
title: "Python's 'yield' and 'yield from'"
date: 2026-02-14
tags: ["python"]
---

```python
# safely opens file without worrying about file size
def read_lines(path):
    with open(path) as f:
        for line in f:
            yield line.strip()

# natural number generator, lazy way
def naturals():
    n = 0
    while True:
        yield n
        n += 1
```

```python
# yield from <iterable>

def flattenA(nested):
    out = []
    for sublist in nested:
        for item in sublist:
            out.append(item)
    return out  # completes flatten at once and returns everything

def flattenB(nested):
    for sublist in nested:
        for item in sublist:
            yield item  # will not continue unless called again

def flattenC(nested):
    for sublist in nested:
        yield from sublist  # treat sublist as a generator, returns one item at a time
```

We can `yield from` an iterable; for example, a generator (e.g., function that uses `yield`), "Lists, Tuples, Strings, Sets, Dicts" (because all of them have `__iter__()` defined), and any object that has `__iter__()` implemented.

```python
yield from 42       # ❌ TypeError
yield from None     # ❌ TypeError
```
