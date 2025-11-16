---
title: "Dijkstra's Algorithm Review"
date: 2025-11-15
tags: ["algorithm", "python"]
---

```python
graph = {
    'A': [('C', 1), ('D', 4)],
    'C': [('D', 2), ('E', 5)],
    'D': [('B', 3)],
    'E': [('B', 1)],
    'B': []  # no outgoing edges
}
```
We want the shortest path A → B. Use Dijkstra.

---

Dijkstra uses three main data structures:  
`dist`: best known distance from A to each node  
`prev`: to reconstruct the path (who is your best predecessor)  
`pq`: min-heap of (distance, node) for the frontier

From start node A:

dist[A] = 0  
dist[others] = float('inf')  
prev[...] = None  
pq = [(0, 'A')] (start with distance 0 to A)  
visited = set() or we just rely on dist checks

```python
dist = {k: float('inf') for k in graph.keys()}
prev = {k: None for k in graph.keys()}
pq = [(0, 'A')]
heapq.heapify(pq)
visited = set()

dist['A'] = 0
```

```python
while pq:
    current_dist, current_node = heapq.heappop(pq)
    
    # Skip if we've already found a better path to this node
    if current_node in visited:
        continue
    
    visited.add(current_node)
    
    # Explore neighbors
    for neighbor, weight in graph[current_node]:
        new_dist = current_dist + weight
        
        # If we found a shorter path, update it
        if new_dist < dist[neighbor]:
            dist[neighbor] = new_dist
            prev[neighbor] = current_node
            heapq.heappush(pq, (new_dist, neighbor))

# Result: shortest distance from A to B
print(f"Shortest distance A → B: {dist['B']}")  # Should be 7

# Reconstruct path
path = []
node = 'B'
while node is not None:
    path.append(node)
    node = prev[node]
path.reverse()
print(f"Path: {' → '.join(path)}")  # Should be A → C → E → B
```

---

edit 11-16:

```python
import heapq

graph = {
    'A': [('C', 1), ('D', 4)],
    'C': [('D', 2), ('E', 5)],
    'D': [('B', 3)],
    'E': [('B', 1)],
    'B': []  # no outgoing edges
}

# shortest path from A to B
def shortest_path_A_to_B(graph: dict):

    dist = {k: float('inf') for k in graph.keys()}
    parent = {k: None for k in graph.keys()}

    dist['A'] = 0
    pq = [(0, 'A')]
    visited = set()

    while pq:
        cur_node_dist, cur_node = heapq.heappop(pq)

        if cur_node in visited:
            continue
        visited.add(cur_node)

        for child_node, child_node_dist in graph[cur_node]:
            possibly_shorter_distance = cur_node_dist + child_node_dist
            if possibly_shorter_distance < dist[child_node]:   # if we can get to child_node in a shorter distance
                dist[child_node] = possibly_shorter_distance
                parent[child_node] = cur_node
                heapq.heappush(pq, (possibly_shorter_distance, child_node))

    return dist['B']

print(shortest_path_A_to_B(graph))
```