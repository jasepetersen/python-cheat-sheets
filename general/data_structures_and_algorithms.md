# Python Data Structures & Algorithms Cheat Sheet

## Stack (LIFO)

```python
stack = []
stack.append(1)
stack.append(2)
stack.pop()     # 2
```

## Queue (FIFO)

```python
from collections import deque

queue = deque()
queue.append(1)
queue.append(2)
queue.popleft()  # 1
```

## Priority Queue / Heap

```python
import heapq

heap = []
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 2)

heapq.heappop(heap)  # 1 (min-heap)
```

Max heap using negatives:

```python
heapq.heappush(heap, -val)
```

## Hash Map

```python
map = {}
map["key"] = "value"
value = map.get("key", None)
```

## Hash Set

```python
s = set()
s.add(1)
s.remove(1)
1 in s  # True or False
```

## Binary Search

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

## DFS (Depth-First Search) - Recursion

```python
def dfs(node, visited):
    if node in visited:
        return
    visited.add(node)
    for neighbor in graph[node]:
        dfs(neighbor, visited)
```

## DFS - Stack (Iterative)

```python
def dfs_iterative(start):
    stack = [start]
    visited = set()
    while stack:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            for neighbor in graph[node]:
                stack.append(neighbor)
```

## BFS (Breadth-First Search)

```python
from collections import deque

def bfs(start):
    queue = deque([start])
    visited = set([start])
    while queue:
        node = queue.popleft()
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

## Backtracking

```python
def backtrack(path, options):
    if done(path):
        results.append(path[:])
        return
    for i, option in enumerate(options):
        path.append(option)
        backtrack(path, options[:i] + options[i+1:])
        path.pop()
```

## Sliding Window

```python
def max_sum_subarray(nums, k):
    max_sum = curr_sum = sum(nums[:k])
    for i in range(k, len(nums)):
        curr_sum += nums[i] - nums[i - k]
        max_sum = max(max_sum, curr_sum)
    return max_sum
```

## Two Pointers

```python
def has_pair_with_sum(arr, target):
    arr.sort()
    left, right = 0, len(arr) - 1
    while left < right:
        s = arr[left] + arr[right]
        if s == target:
            return True
        elif s < target:
            left += 1
        else:
            right -= 1
    return False
```

## Union Find (Disjoint Set)

```python
class UnionFind:
    def __init__(self, size):
        self.root = list(range(size))

    def find(self, x):
        if self.root[x] != x:
            self.root[x] = self.find(self.root[x])
        return self.root[x]

    def union(self, x, y):
        rootX, rootY = self.find(x), self.find(y)
        if rootX != rootY:
            self.root[rootY] = rootX
```

## Topological Sort (Kahn’s Algorithm)

```python
from collections import deque, defaultdict

def topological_sort(graph):
    in_degree = defaultdict(int)
    for u in graph:
        for v in graph[u]:
            in_degree[v] += 1

    queue = deque([u for u in graph if in_degree[u] == 0])
    result = []

    while queue:
        u = queue.popleft()
        result.append(u)
        for v in graph[u]:
            in_degree[v] -= 1
            if in_degree[v] == 0:
                queue.append(v)

    return result
```

## Trie (Prefix Tree)

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        cur = self.root
        for ch in word:
            if ch not in cur.children:
                cur.children[ch] = TrieNode()
            cur = cur.children[ch]
        cur.end = True

    def search(self, word):
        cur = self.root
        for ch in word:
            if ch not in cur.children:
                return False
            cur = cur.children[ch]
        return cur.end
```
