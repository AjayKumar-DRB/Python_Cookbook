# Concurrency Basics

> Threads, Processes, and the GIL.

---

## Introduction

If you are interviewing for a backend Python role, the interviewer will almost certainly ask you about concurrency. 

Python's approach to concurrency is unique (and often criticized) due to a specific architectural choice made in the 1990s: the Global Interpreter Lock (GIL). You must understand this thoroughly.

---

## The Global Interpreter Lock (GIL)

In Python (specifically CPython, the standard implementation), the GIL is a mutex that protects access to Python objects, preventing multiple threads from executing Python bytecodes at once.

**What this means:** Even if your computer has 16 CPU cores, a multi-threaded Python program will only ever execute on ONE core at a time. The GIL prevents true parallel execution of Python code.

---

## When to use Multithreading (`threading`)

If the GIL prevents true parallelism, why does the `threading` module exist?

Because the GIL is released during **I/O operations** (like waiting for a network request, downloading a file, or waiting for a database query to return).

- **Use Case:** I/O Bound tasks (Web scraping, API calls, File I/O).
- **Result:** While Thread A is waiting for a website to respond, it releases the GIL. Thread B can acquire the GIL and send its own request. This massively speeds up I/O bound scripts.

```python
import threading
import requests

def fetch_url(url):
    response = requests.get(url)
    print(response.status_code)

# These will run concurrently, speeding up the total execution time
t1 = threading.Thread(target=fetch_url, args=("http://example.com",))
t2 = threading.Thread(target=fetch_url, args=("http://example.org",))
t1.start()
t2.start()
t1.join()
t2.join()
```

---

## When to use Multiprocessing (`multiprocessing`)

If you have a **CPU Bound** task (like processing millions of images, rendering 3D graphics, or running heavy math calculations), multithreading will actually make your program *slower* due to the overhead of switching threads while still being bound by the GIL.

To bypass the GIL, you must use the `multiprocessing` module. This spawns entirely separate Python processes, each with its own memory space and its own GIL.

- **Use Case:** CPU Bound tasks.
- **Result:** True parallelism across multiple CPU cores.
- **Downside:** Processes do not share memory. Passing data between them requires serialization (Pickling) and Inter-Process Communication (IPC), which has significant overhead.

```python
import multiprocessing

def heavy_computation(num):
    # This will run on a separate CPU core
    return sum(i * i for i in range(num))

if __name__ == '__main__':
    with multiprocessing.Pool(processes=4) as pool:
        results = pool.map(heavy_computation, [10**7, 10**7, 10**7])
```

---

## Asyncio (`asyncio`)

Python 3.4 introduced `asyncio`, which provides single-threaded, concurrent code using coroutines (`async` / `await`). 

Unlike threading (where the OS preemptively switches context), `asyncio` uses cooperative multitasking (the code explicitly yields control back to the event loop using `await`).

- **Use Case:** Extremely high-volume I/O (like handling 10,000 simultaneous websocket connections in a chat server).
- **Benefit:** Massive scalability with very low memory overhead compared to spawning 10,000 OS threads.

---

## Key Takeaways

If an interviewer asks: *"How do you make Python code run faster?"*
1. **I/O Bound?** Use `asyncio` or `threading` (GIL is released).
2. **CPU Bound?** Use `multiprocessing` to bypass the GIL, or rewrite the hot loop in C/Rust (using Cython or PyO3).

---

## Related Topics

- [System Design Primer](06-system-design-primer.md)
