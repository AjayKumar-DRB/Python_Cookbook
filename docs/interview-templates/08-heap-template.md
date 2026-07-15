# Heap (Priority Queue) Template

## Top-K Elements Template

When asked to find the Top $K$ largest elements, maintain a Min-Heap of size exactly $K$.

```python
import heapq

def find_top_k(nums, k):
    min_heap = []
    
    for num in nums:
        # Push to heap
        heapq.heappush(min_heap, num)
        
        # If heap exceeds size K, pop the smallest element
        if len(min_heap) > k:
            heapq.heappop(min_heap)
            
    # The heap now contains exactly the K largest elements
    return min_heap
```

## Max-Heap Template

Python does not have a native Max-Heap. You must invert the numbers by multiplying by `-1`.

```python
import heapq

def max_heap_example(nums):
    max_heap = []
    
    for num in nums:
        # Push negative value!
        heapq.heappush(max_heap, -num)
        
    result = []
    while max_heap:
        # Pop and negate back to original positive value!
        largest = -heapq.heappop(max_heap)
        result.append(largest)
        
    return result
```

## Crucial Reminders
1. **Always `import heapq`**.
2. **In-Place Heapify**: If you need to turn an entire existing array into a heap, do not loop and push. Use `heapq.heapify(nums)`, which runs in $O(N)$ time instead of $O(N \log N)$.
3. **Tuples in Heaps**: If you push tuples into a heap (e.g., `(priority, value)`), Python will sort by the `priority`. If two items tie on priority, it will compare the `value`s. If the `value`s are custom objects that cannot be compared, Python will throw a `TypeError`.
