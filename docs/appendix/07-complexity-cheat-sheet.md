# Complexity Cheat Sheet

## Python Built-in Data Structures

### Lists (Dynamic Arrays)
| Operation | Average Case | Amortized Worst Case |
| :--- | :---: | :---: |
| Copy | $O(N)$ | $O(N)$ |
| Append `[1]` | $O(1)$ | $O(1)$ |
| Pop last | $O(1)$ | $O(1)$ |
| Pop first | $O(N)$ | $O(N)$ |
| Insert `[1]` | $O(N)$ | $O(N)$ |
| Get Item | $O(1)$ | $O(1)$ |
| Set Item | $O(1)$ | $O(1)$ |
| Delete Item | $O(N)$ | $O(N)$ |
| Iteration | $O(N)$ | $O(N)$ |
| Get Slice | $O(K)$ | $O(K)$ |
| Del Slice | $O(N)$ | $O(N)$ |
| Set Slice | $O(K+N)$ | $O(K+N)$ |
| Extend `[1]` | $O(K)$ | $O(K)$ |
| Sort | $O(N \log N)$ | $O(N \log N)$ |
| Multiply | $O(NK)$ | $O(NK)$ |
| `x in s` | $O(N)$ | $O(N)$ |
| `min(s)`, `max(s)` | $O(N)$ | $O(N)$ |
| Get Length | $O(1)$ | $O(1)$ |

### Dictionaries (Hash Tables)
| Operation | Average Case | Amortized Worst Case |
| :--- | :---: | :---: |
| Copy | $O(N)$ | $O(N)$ |
| Get Item | $O(1)$ | $O(N)$ |
| Set Item | $O(1)$ | $O(N)$ |
| Delete Item | $O(1)$ | $O(N)$ |
| Iteration | $O(N)$ | $O(N)$ |
| `x in s` | $O(1)$ | $O(N)$ |

### Sets (Hash Tables)
| Operation | Average Case | Amortized Worst Case |
| :--- | :---: | :---: |
| `x in s` | $O(1)$ | $O(N)$ |
| Union `s \| t` | $O(len(s) + len(t))$ | |
| Intersection `s & t` | $O(min(len(s), len(t)))$ | $O(len(s) * len(t))$ |
| Multiple intersection | $O(N_1 * min(N_2, ..., N_k))$ | |
| Difference `s - t` | $O(len(s))$ | |
| Symmetric Difference `s ^ t`| $O(len(s))$ | $O(len(s) * len(t))$ |

## Standard Algorithms

### Sorting
| Algorithm | Time (Best) | Time (Average) | Time (Worst) | Space |
| :--- | :---: | :---: | :---: | :---: |
| **Quicksort** | $\Omega(N \log N)$ | $\Theta(N \log N)$ | $O(N^2)$ | $O(\log N)$ |
| **Mergesort** | $\Omega(N \log N)$ | $\Theta(N \log N)$ | $O(N \log N)$ | $O(N)$ |
| **Timsort (Python)** | $\Omega(N)$ | $\Theta(N \log N)$ | $O(N \log N)$ | $O(N)$ |
| **Heapsort** | $\Omega(N \log N)$ | $\Theta(N \log N)$ | $O(N \log N)$ | $O(1)$ |
| **Bubble Sort** | $\Omega(N)$ | $\Theta(N^2)$ | $O(N^2)$ | $O(1)$ |

### Graph Traversal
$V$ = Vertices, $E$ = Edges
- **DFS / BFS**: $O(V + E)$ Time, $O(V)$ Space
- **Topological Sort**: $O(V + E)$ Time, $O(V)$ Space
- **Dijkstra**: $O((V + E) \log V)$ Time, $O(V)$ Space

### Tree Operations (Binary Search Tree)
- **Search / Insert / Delete**: $O(\log N)$ Average, $O(N)$ Worst
- **Traversal (In-order, Pre-order)**: $O(N)$ Time, $O(N)$ Space
