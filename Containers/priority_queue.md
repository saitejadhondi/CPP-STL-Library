# C++ STL - Priority Queue (`std::priority_queue`)

> Interview-focused notes on the C++ STL Priority Queue.

------------------------------------------------------------------------

# What is a Priority Queue?

A **Priority Queue** is a container adaptor where the element with the
**highest priority** is always available at the top.

By default, C++ implements it as a **Max Heap**.

Unlike a normal queue (FIFO), elements are removed based on
**priority**, not insertion order.

Example:

    Insert: 5 1 10 3

    Top -> 10

    Pop()

    Top -> 5

------------------------------------------------------------------------

# Internal Implementation

`std::priority_queue` is implemented using a **Binary Heap** (stored
internally in a vector).

Binary Heap Properties:

-   Complete Binary Tree
-   Parent has higher priority than children (Max Heap)

Example:

            10
          /    \
         5      8
        / \
       1   3

------------------------------------------------------------------------

# Applications

-   Dijkstra's Algorithm
-   Prim's Algorithm
-   Huffman Coding
-   Job Scheduling
-   Event Simulation
-   Top K Problems
-   Kth Largest/Smallest Element
-   Median of Data Stream

------------------------------------------------------------------------

# Declaration

## Max Heap (Default)

``` cpp
#include <queue>

priority_queue<int> pq;
```

## Min Heap

``` cpp
priority_queue<int, vector<int>, greater<int>> pq;
```

------------------------------------------------------------------------

# Important Functions

## push()

``` cpp
pq.push(10);
pq.push(5);
pq.push(20);
```

Time Complexity: **O(log n)**

------------------------------------------------------------------------

## pop()

Removes the highest-priority element.

``` cpp
pq.pop();
```

Time Complexity: **O(log n)**

------------------------------------------------------------------------

## top()

Returns the highest-priority element.

``` cpp
cout << pq.top();
```

Time Complexity: **O(1)**

------------------------------------------------------------------------

## size()

``` cpp
pq.size();
```

Time Complexity: **O(1)**

------------------------------------------------------------------------

## empty()

``` cpp
pq.empty();
```

Time Complexity: **O(1)**

------------------------------------------------------------------------

# Max Heap Example

``` cpp
priority_queue<int> pq;

pq.push(6);
pq.push(10);
pq.push(3);
pq.push(8);

while(!pq.empty())
{
    cout<<pq.top()<<" ";
    pq.pop();
}
```

Output

    10 8 6 3

------------------------------------------------------------------------

# Min Heap Example

``` cpp
priority_queue<int, vector<int>, greater<int>> pq;

pq.push(6);
pq.push(10);
pq.push(3);
pq.push(8);

while(!pq.empty())
{
    cout<<pq.top()<<" ";
    pq.pop();
}
```

Output

    3 6 8 10

------------------------------------------------------------------------

# Priority Queue of Pairs

Default comparison:

``` cpp
priority_queue<pair<int,int>> pq;
```

Comparison order:

1.  First element
2.  Second element (if first is equal)

Example:

    (5,2)
    (5,8)
    (7,1)

    Top

    (7,1)

------------------------------------------------------------------------

# Custom Comparator

Ascending based on second value:

``` cpp
struct Compare
{
    bool operator()(pair<int,int> a,
                    pair<int,int> b)
    {
        return a.second > b.second;
    }
};

priority_queue<
pair<int,int>,
vector<pair<int,int>>,
Compare> pq;
```

Useful for graph algorithms and scheduling problems.

------------------------------------------------------------------------

# Traversing

A priority queue cannot be traversed using indexing or iterators.

Use:

``` cpp
priority_queue<int> temp = pq;

while(!temp.empty())
{
    cout<<temp.top()<<" ";
    temp.pop();
}
```

------------------------------------------------------------------------

# Complete Example

``` cpp
#include<iostream>
#include<queue>

using namespace std;

int main()
{
    priority_queue<int> pq;

    pq.push(10);
    pq.push(5);
    pq.push(30);
    pq.push(20);

    cout<<pq.top()<<endl;

    pq.pop();

    cout<<pq.top()<<endl;

    cout<<pq.size()<<endl;

    cout<<pq.empty()<<endl;
}
```

Output

    30
    20
    3
    0

------------------------------------------------------------------------

# Time Complexity

  Operation   Complexity
  ----------- ------------
  push()      O(log n)
  pop()       O(log n)
  top()       O(1)
  size()      O(1)
  empty()     O(1)

------------------------------------------------------------------------

# Queue vs Priority Queue

  Queue            Priority Queue
  ---------------- ------------------------
  FIFO             Highest Priority First
  front()          top()
  O(1) insertion   O(log n) insertion

------------------------------------------------------------------------

# Heap vs Priority Queue

  Heap                     Priority Queue
  ------------------------ -----------------------
  Data Structure           STL Container Adaptor
  Can implement manually   Uses heap internally

------------------------------------------------------------------------

# Interview Questions

## Why is push() O(log n)?

After insertion, the new element moves upward (heapify-up), taking at
most the height of the heap.

------------------------------------------------------------------------

## Why is top() O(1)?

The maximum (or minimum) element is always stored at the root.

------------------------------------------------------------------------

## Does Priority Queue keep elements sorted?

No.

Only the top element is guaranteed to have the highest (or lowest)
priority.

------------------------------------------------------------------------

## How to create a Min Heap?

``` cpp
priority_queue<int, vector<int>, greater<int>> pq;
```

------------------------------------------------------------------------

# Common Coding Problems

1.  Kth Largest Element
2.  Top K Frequent Elements
3.  Merge K Sorted Lists
4.  Merge K Sorted Arrays
5.  Dijkstra's Algorithm
6.  Prim's MST
7.  Reorganize String
8.  Task Scheduler
9.  Find Median from Data Stream
10. Last Stone Weight

------------------------------------------------------------------------

# Tips

-   Default priority queue is a **Max Heap**.
-   Use `greater<T>` to create a **Min Heap**.
-   `top()` does not remove the element.
-   `pop()` removes but does not return the element.
-   Ideal for problems involving **Top K**, **greedy algorithms**, and
    **graph shortest paths**.
