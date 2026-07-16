# C++ STL - Queue (`std::queue`)

> Interview-focused notes on the C++ STL Queue.

------------------------------------------------------------------------

## Learning path

- Previous: [Stack](stack.md)
- Next: [Deque](deque.md)
- Related: [Priority Queue](priority_queue.md), [Vector](vector.md)

------------------------------------------------------------------------

# What is a Queue?

A **queue** is a linear data structure that follows the **FIFO (First
In, First Out)** principle.

The first element inserted is the first one removed.

Example:

    Push: 10
    Push: 20
    Push: 30

    Front -> 10

    Pop()

    Front -> 20

Think of people standing in a line at a ticket counter. The first person
to join the line is served first.

------------------------------------------------------------------------

# Where is Queue Used?

-   CPU Scheduling
-   Printer Queue
-   Task Scheduling
-   Breadth First Search (BFS)
-   Network Packet Processing
-   Producer-Consumer Problems
-   Customer Service Systems

------------------------------------------------------------------------

# Declaration

``` cpp
#include <queue>

queue<int> q;
queue<string> q2;
queue<pair<int,int>> q3;
```

------------------------------------------------------------------------

# FIFO Visualization

    Front                        Back

    10   20   30   40

    ^                  ^
    Remove Here        Insert Here

-   Insertion always happens at the **back**
-   Deletion always happens from the **front**

------------------------------------------------------------------------

# Important Functions

## push()

Adds an element at the back.

``` cpp
q.push(10);
q.push(20);
q.push(30);
```

Queue:

    Front

    10 20 30

    Back

Time Complexity: **O(1)**

------------------------------------------------------------------------

## pop()

Removes the front element.

``` cpp
q.pop();
```

Queue becomes

    20 30

> Like `stack::pop()`, it does **not** return the removed element.

Time Complexity: **O(1)**

------------------------------------------------------------------------

## front()

Returns the first element.

``` cpp
cout << q.front();
```

Output

    10

Time Complexity: **O(1)**

------------------------------------------------------------------------

## back()

Returns the last element.

``` cpp
cout << q.back();
```

Output

    30

Time Complexity: **O(1)**

------------------------------------------------------------------------

## size()

Returns the number of elements.

``` cpp
q.size();
```

Time Complexity: **O(1)**

------------------------------------------------------------------------

## empty()

Checks whether the queue is empty.

``` cpp
q.empty();
```

Returns `true` or `false`.

Time Complexity: **O(1)**

------------------------------------------------------------------------

# Traversing a Queue

Queues do not support indexing or iterators.

Use a temporary copy if you want to print the contents without modifying
the original queue.

``` cpp
queue<int> temp = q;

while(!temp.empty())
{
    cout << temp.front() << " ";
    temp.pop();
}
```

------------------------------------------------------------------------

# Complete Example

``` cpp
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<int> q;

    q.push(10);
    q.push(20);
    q.push(30);

    cout << q.front() << endl;
    cout << q.back() << endl;

    q.pop();

    cout << q.front() << endl;

    cout << q.size() << endl;

    cout << q.empty() << endl;

    return 0;
}
```

Output

    10
    30
    20
    2
    0

------------------------------------------------------------------------

# Time Complexity

  Operation   Complexity
  ----------- ------------
  push()      O(1)
  pop()       O(1)
  front()     O(1)
  back()      O(1)
  size()      O(1)
  empty()     O(1)

------------------------------------------------------------------------

# Queue vs Stack

  Queue              Stack
  ------------------ ----------------
  FIFO               LIFO
  push() at Back     push() at Top
  pop() from Front   pop() from Top
  front()            top()

------------------------------------------------------------------------

# Queue vs Deque

  Queue                  Deque
  ---------------------- ------------------------
  Insert only at Back    Insert at Front & Back
  Delete only at Front   Delete at Front & Back
  Restricted             More Flexible

------------------------------------------------------------------------

# Underlying Container

By default:

``` cpp
deque<T>
```

You may also use:

``` cpp
queue<int, list<int>> q;
```

------------------------------------------------------------------------

# Interview Questions

## Why can't we access the middle element?

Queue exposes only the **front** and **back** to preserve FIFO behavior.

------------------------------------------------------------------------

## Does pop() return the removed value?

No.

``` cpp
q.pop();
```

returns **void**.

Use

``` cpp
q.front();
```

before calling `pop()`.

------------------------------------------------------------------------

## What happens if front() is called on an empty queue?

It results in **undefined behavior**.

Always check

``` cpp
if(!q.empty())
```

before accessing `front()` or `back()`.

------------------------------------------------------------------------

# Common Coding Problems

1.  Implement Queue using Stacks
2.  Implement Stack using Queues
3.  BFS Traversal
4.  Rotten Oranges
5.  Binary Tree Level Order Traversal
6.  Generate Binary Numbers
7.  Sliding Window Maximum (Deque variant)
8.  Circular Queue
9.  First Non-Repeating Character in Stream
10. Josephus Problem (Queue approach)

------------------------------------------------------------------------

# Tips

-   Queue is one of the most important STL containers for graph
    algorithms.
-   `pop()` removes but does not return the element.
-   Use `front()` before `pop()`.
-   Never call `front()` or `back()` on an empty queue.
-   Queue does not support random access or iterators.
