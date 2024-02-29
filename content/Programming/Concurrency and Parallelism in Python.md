---
tags:
  - programming-language
---
### What is concurrency?

[Concurrency](https://en.wikipedia.org/wiki/Concurrency_(computer_science)) is the ability of a program to handle **multiple task or activities** seemingly **at the same time** (execution of multiple tasks or processes in overlapping time periods)

![[Concurrency.png]]
> Visualization of multi-threading method

>[!Example]
> Imagine we have two tasks to do
> - Read a book
> - Eat sandwich
> 
> For concurrency, You can start both task at the same time, but you can **only focus on one at a time**, you might read a book, then switch to eat our sandwich, then back to read a book, and so on.
> 
> It feel like we're doing both at once, but we're really just switching quickly between them.

Maybe some of us here know about `multi-threading` but that method is not the only way to perform concurrency, we will talk about it in the later section.

What about **parallelism**, what is the difference?

### Parallelism and its difference with concurrency

[Parallelism](https://en.wikipedia.org/wiki/Data_parallelism) is the ability to **perform multiple tasks simultaneously**, using multiple processor

![[Parallelism.png]]
> Visualization of multi-processing method

>[!Example]
>For parallelism, we have friend to help us. Let use the previous case, where we need to read a book and eat sandwich. Your friend will read a book while we eat sandwich **at the same time**.

#### Difference

| Concurrency                                                 | Parallelism                                             |
| ----------------------------------------------------------- | ------------------------------------------------------- |
| Focuses on managing multiple tasks                          | Focuses on dividing a single task into smaller subtasks |
| Can be achieved on a single processor                       | Requires multiple processors or cores                   |
| No two parts might run at the **exactly same time**         | Multiple parts can be executed at the same time         |
| Task might share information with each other when necessary | Typically **don't directly share information**          |
### I/O-bound vs CPU-Bound

Before we learn about concurrency, we need to know two important concepts: **I/O-bound vs CPU-Bound**

>*I/O-bound task* spend a significant portion of their time **waiting for input or output operations**.
>
>*CPU-bound tasks* heavily utilize the **processing power of the CPU**. for examples, complex calculations.

| Feature        | I/O-Bound                                                                                | CPU-Bound                                                        |
| -------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **Definition** | Processes that spend most of their time waiting for input/output operations to complete. | Processes that spend most of their time performing calculations. |
| **Bottleneck** | Speed of input/output systems (e.g., hard disks, network, user interfaces)               | Speed of the processor (CPU)                                     |
| **Behavior**   | Frequently wait for external resources, potentially leaving the CPU idle.                | Utilize the CPU heavily, often reaching maximum usage.           |
| **Examples**   | * Downloading/uploading large files                                                      | * Complex scientific computations                                |
|                | * Reading data from a database                                                           | * Video encoding/decoding                                        |
|                | * Sending network requests                                                               | * 3D graphics rendering                                          |
|                | * Waiting for user input                                                                 | * Sorting large arrays of numbers                                |

### GIL (Global Interpreter Lock)

[Global Interpreter Lock](https://en.wikipedia.org/wiki/Global_interpreter_lock) is mechanism that make sure that **only one thread can use python interpreter at a time**. Python will block other thread that try to access interpreter while other thread is currently executed. Gil limits true parallelism in multi-core systems.

![[GIL_description.gif]]

> Red - Blocked Thread
> 
> Green - Thread currently work under GIL

##### Purpose of GIL

*GIL* has its advantage. It ensures memory safety and thread security by letting only one thread execute Python code at a time.

It help simplify the memory management of Python objects. Python memory management use [reference counting](https://en.wikipedia.org/wiki/Reference_counting) as its primary technique, each object store count of references pointing to it and when count of an object equal to zero, it is deallocated. GIL make sure that only one thread can modify this *reference count* at a time.

### Concurrency in Python

##### Multithreading

Technique where operating system switches between active threads at very high speed, giving the illusion that they are executing simultaneously

###### Keywords

![[Processes.png]]
> This picture above show us about process and thread relation

| Term                  | Definition                                                                                                        |
| --------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Thread**            | A lightweight unit of execution within a process.                                                                 |
| **Context Switching** | The process of saving the state of one thread and restoring the state of another, allowing them to share the CPU. |
| **Synchronization**   | Coordinating actions and timing of multiple threads to ensure proper access to shared resources.                  |
###### Example

This example is an **I/O-bound** with no concurrency

```python
import time
import requests

urls = ["https://dummyjson.com/products", "https://dummyjson.com/products"]

def fetch_data(url):
    response = requests.get(url)
    print(f"Data from {url} received")

begin = time.time()
for url in urls:
    fetch_data(url)
end = time.time()
  
print("Used time:", end-begin, "seconds")
```

```shell
Data from https://dummyjson.com/products received
Data from https://dummyjson.com/products received
Used time:  1.7840371131896973 seconds
```

This code fetch data from the provided *URLs*. We have to wait for the first one to finish loading first so it can be slow if data is large.

We will use our data fetching example but we're going to use [threading](https://docs.python.org/3/library/threading.html#module-threading) module.

```python
import requests
import threading
import time

urls = ["https://dummyjson.com/products", "https://dummyjson.com/products"]
def fetch_data(url):
    response = requests.get(url)
    print(f"Data from {url} received")

threads = [threading.Thread(target=fetch_data, args=(url,)) for url in urls]

begin = time.time()
for thread in threads:
    thread.start()

for thread in threads:
    thread.join()
end = time.time()

print("Used time:", end-begin, "seconds")
```

```shell
Data from https://dummyjson.com/products received
Data from https://dummyjson.com/products received
Used time: 0.6703526973724365 seconds
```

Output from **multi-threading** method take shorter time than normal sequential method. For I/O-bound task multi-threading help us with performance.

>[!Question] What is the difference between _thread, threading and concurrent.futures]
> - [_thread](https://docs.python.org/3/library/_thread.html#module-_thread) : provides low-level primitives for working with multiple threads
> - [threading](https://docs.python.org/3/library/threading.html#module-threading) : threading interfaces on top of the lower level [`_thread`](https://docs.python.org/3/library/_thread.html#module-_thread "_thread: Low-level threading API.") module
> - [concurrent.futures](https://docs.python.org/3/library/concurrent.futures.html#module-concurrent.futures) : module provides a high-level interface for asynchronously executing callables

###### Threading Problems

When thread can access to shared memory, it can bring us some problems

**Race Condition**

**Most likely to occur** when **multiple threads attempt to **read or write** the same shared data** at the same time **without proper synchronization**

![[Race_Condition.png]]

> Imagine that we have bank account program with 100$ in it. Two thread try to withdraw $80 each. If there's a race condition, it's possible _both_ threads might see the $100 balance and think it's safe, withdrawn the money, make our account go negative. 

we can prevent this with good **locking mechanisms**

**Deadlock**

Occur when **two or more threads are each waiting for a resource** that is **currently held by another waiting thread**.

> Imagine us and our friends both grabbing onto the same toy and refusing to let go. Two or more threads get stuck waiting for each other to release a resource, essentially freezing the program

##### Coroutines

[Coroutines](https://en.wikipedia.org/wiki/Coroutine) is a special kind of function whose execution can be paused and resumed multiple times. Usually, it use `async` and `await` keywords to define + handle asynchronous behavior

>[!tip] Relation between subroutine and coroutine
> Coroutines **extend the concept of subroutines** with the capability of pausing and resuming execution.
###### Keywords

| Keyword/Concept      | Definition                                         | Purpose                                                                                                                   |
| -------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **awaitable object** | An object that can be used with `await`            | Represents a task that can be asynchronously awaited and potentially yield a result.                                      |
| **Event loop**       | An essential component in asynchronous programming | Manages the execution of coroutines, scheduling them to run and handling their pauses and resumes. (when A happens, do B) |
###### How does `async` and `await` work?

`async` define a coroutine function and `await` pauses the current coroutine's execution and returns control to the event loop until the awaited task completes.

For more detail, please visit [How-the-heck-does-async-await-work](https://snarky.ca/how-the-heck-does-async-await-work-in-python-3-5/)
###### Example

First of all, we need to install [aiohttp](https://docs.aiohttp.org/en/stable/)

```shell
pip install aiohttp
```

We will use same situation as multi-threading example.

```python
import aiohttp
import asyncio
import time

async def fetch_data(session, url):
    async with session.get(url) as response:
        data = await response.text()
        print(f"Data from {url} received")
        return data

async def main():
    url = "https://dummyjson.com/products"
    async with aiohttp.ClientSession() as session:
        await fetch_data(session, url)
        await fetch_data(session, url)

begin = time.time()
asyncio.run(main())
end = time.time()

print("Used time:", end-begin, "seconds")
```

```Output
Data from https://dummyjson.com/products received
Data from https://dummyjson.com/products received
Used time: 0.8993885517120361 seconds
```

