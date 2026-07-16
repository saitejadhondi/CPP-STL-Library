# C++ STL - Deque (`std::deque`)

> Interview-focused notes on the C++ STL Deque.

------------------------------------------------------------------------

## Learning path

- Previous: [Queue](queue.md)
- Next: [Priority Queue](priority_queue.md)
- Related: [Vector](vector.md), [Stack](stack.md)

------------------------------------------------------------------------

# What is a Deque?

A **Deque (Double Ended Queue)** is a sequence container that allows
insertion and deletion from **both the front and the back** efficiently.

It combines the advantages of both **Vector** and **Queue**.

Unlike `std::vector`, a deque does not store all elements in one
continuous memory block. Instead, it uses multiple fixed-size memory
blocks managed internally, allowing efficient insertions at both ends.

------------------------------------------------------------------------

# Why is it called Double Ended Queue?

Because operations can be performed from **both ends**.

    Front                           Back

    10 20 30 40 50

    ↑               ↑

    Insert/Delete   Insert/Delete

------------------------------------------------------------------------

# Where is Deque Used?

-   Sliding Window Maximum
-   Monotonic Queue
-   Browser History
-   Undo/Redo
-   Task Scheduling
-   Palindrome Checking
-   Cache Implementations

------------------------------------------------------------------------

# Internal Memory Layout

Unlike vectors

    Vector

    ----------------------------
    10 20 30 40 50
    ----------------------------

Deque stores elements like

    Block 1       Block 2       Block 3

    10 20 30 | 40 50 60 | 70 80

A small map of pointers connects these blocks.

Advantages

-   Fast insertion at front
-   Fast insertion at back
-   Constant time indexing

Disadvantage

-   Slightly slower random access than vector.

------------------------------------------------------------------------

# Declaration

``` cpp
#include <deque>

deque<int> dq;

deque<int> dq2(5);

deque<int> dq3(5,100);

deque<int> dq4={1,2,3,4};
```

------------------------------------------------------------------------

# Important Functions

## push_back()

``` cpp
dq.push_back(10);
dq.push_back(20);
```

    10 20

Time Complexity

    O(1)

------------------------------------------------------------------------

## push_front()

``` cpp
dq.push_front(5);
```

    5 10 20

Time Complexity

    O(1)

------------------------------------------------------------------------

## pop_back()

Removes the last element.

``` cpp
dq.pop_back();
```

    5 10

Time Complexity

    O(1)

------------------------------------------------------------------------

## pop_front()

Removes the first element.

``` cpp
dq.pop_front();
```

    10

Time Complexity

    O(1)

------------------------------------------------------------------------

## front()

``` cpp
dq.front();
```

Returns first element.

------------------------------------------------------------------------

## back()

``` cpp
dq.back();
```

Returns last element.

------------------------------------------------------------------------

## at()

``` cpp
dq.at(2);
```

Performs bounds checking.

------------------------------------------------------------------------

## operator\[\]

``` cpp
dq[2];
```

No bounds checking.

------------------------------------------------------------------------

## insert()

``` cpp
dq.insert(dq.begin()+2,100);
```

Time Complexity

    O(n)

------------------------------------------------------------------------

## erase()

``` cpp
dq.erase(dq.begin()+1);
```

Time Complexity

    O(n)

------------------------------------------------------------------------

## clear()

``` cpp
dq.clear();
```

Removes all elements.

------------------------------------------------------------------------

## size()

``` cpp
dq.size();
```

Returns number of elements.

------------------------------------------------------------------------

## empty()

``` cpp
dq.empty();
```

Returns true if deque is empty.

------------------------------------------------------------------------

# Traversing a Deque

## Index

``` cpp
for(int i=0;i<dq.size();i++)
    cout<<dq[i];
```

------------------------------------------------------------------------

## Range-based Loop

``` cpp
for(auto x:dq)
    cout<<x;
```

------------------------------------------------------------------------

## Iterator

``` cpp
for(auto it=dq.begin();it!=dq.end();it++)
    cout<<*it;
```

------------------------------------------------------------------------

# Complete Example

``` cpp
#include<iostream>
#include<deque>

using namespace std;

int main()
{
    deque<int> dq;

    dq.push_back(20);
    dq.push_back(30);

    dq.push_front(10);

    dq.push_front(5);

    for(auto x:dq)
        cout<<x<<" ";

    cout<<endl;

    dq.pop_front();

    dq.pop_back();

    for(auto x:dq)
        cout<<x<<" ";

    return 0;
}
```

Output

    5 10 20 30

    10 20

------------------------------------------------------------------------

# Time Complexity

  Operation      Complexity
  -------------- ------------
  push_back()    O(1)
  push_front()   O(1)
  pop_back()     O(1)
  pop_front()    O(1)
  front()        O(1)
  back()         O(1)
  operator\[\]   O(1)
  at()           O(1)
  insert()       O(n)
  erase()        O(n)
  size()         O(1)
  empty()        O(1)

------------------------------------------------------------------------

# Vector vs Deque

  Feature             Vector       Deque
  ------------------- ------------ ----------
  Random Access       ⭐⭐⭐⭐⭐   ⭐⭐⭐⭐
  push_back()         O(1)         O(1)
  push_front()        O(n)         O(1)
  Contiguous Memory   Yes          No
  Memory Overhead     Low          Higher

------------------------------------------------------------------------

# Queue vs Deque

  Queue          Deque
  -------------- -----------
  Insert Back    Both Ends
  Delete Front   Both Ends
  Restricted     Flexible

------------------------------------------------------------------------

# Iterator Invalidation

-   `push_front()` and `push_back()` may invalidate iterators.
-   Insertion in the middle invalidates iterators.
-   Erase invalidates iterators to erased elements.

------------------------------------------------------------------------

# Interview Questions

## Why not always use deque instead of vector?

Although deque supports more operations efficiently, vector provides: -
Better cache locality - Faster iteration - Better random access
performance - Lower memory overhead

Hence vector is preferred whenever insertion at the front is not
required.

------------------------------------------------------------------------

## Does deque have contiguous memory?

No.

It stores elements in multiple blocks.

------------------------------------------------------------------------

## Which STL container uses deque internally?

-   Stack
-   Queue

By default

``` cpp
stack<int>

queue<int>
```

internally use

``` cpp
deque<int>
```

------------------------------------------------------------------------

# Common Coding Problems

1.  Sliding Window Maximum
2.  Shortest Subarray with Sum at Least K
3.  Monotonic Queue
4.  Circular Buffer
5.  Design Front Middle Back Queue
6.  Moving Average from Data Stream
7.  Design Browser History

------------------------------------------------------------------------

# Tips

-   Use deque whenever insertions and deletions happen at both ends.
-   Prefer vector for heavy iteration and cache-friendly operations.
-   Deque is the default underlying container for both `stack` and
    `queue`.
