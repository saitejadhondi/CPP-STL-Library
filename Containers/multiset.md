# C++ STL - Multiset (`std::multiset`)

> Interview-focused notes on the C++ STL Multiset.

------------------------------------------------------------------------

## Learning path

- Previous: [Unordered Set](unordered_set.md)
- Next: [Unordered Multiset](unordered_multiset.md)
- Related: [Set](set.md), [Map](map.md)

------------------------------------------------------------------------

# What is a Multiset?

A **multiset** is an ordered associative container that stores elements
in **sorted order** and **allows duplicate values**.

It is implemented internally using a **Red-Black Tree**.

Example:

``` cpp
multiset<int> ms;

ms.insert(10);
ms.insert(10);
ms.insert(20);
ms.insert(5);
```

Output:

    5 10 10 20

Unlike `set`, duplicates are preserved.

------------------------------------------------------------------------

# When to Use?

Use `multiset` when:

-   Duplicate values matter.
-   Data must remain sorted.
-   Fast insertion, deletion and searching are required.

Applications:

-   Frequency tracking
-   Sliding window median
-   Event scheduling
-   Ranking systems
-   Competitive programming

------------------------------------------------------------------------

# Internal Working

`multiset` uses a self-balancing **Red-Black Tree**.

Properties:

-   Automatically sorted
-   Allows duplicate keys
-   Height remains O(log n)

------------------------------------------------------------------------

# Declaration

``` cpp
#include <set>

multiset<int> ms;
multiset<string> names;
multiset<pair<int,int>> pts;

// Descending order
multiset<int, greater<int>> ms2;
```

------------------------------------------------------------------------

# Important Functions

## insert()

``` cpp
ms.insert(10);
ms.insert(10);
ms.insert(20);
```

Output:

    10 10 20

Time Complexity: **O(log n)**

------------------------------------------------------------------------

## emplace()

``` cpp
ms.emplace(30);
```

Constructs the object directly in place.

------------------------------------------------------------------------

## erase(key)

``` cpp
ms.erase(10);
```

Removes **all occurrences** of `10`.

Example:

    10 10 10 20

    ↓

    20

------------------------------------------------------------------------

## erase(iterator)

``` cpp
auto it = ms.find(10);

ms.erase(it);
```

Removes **only one occurrence**.

    10 10 10 20

    ↓

    10 10 20

------------------------------------------------------------------------

## find()

``` cpp
auto it = ms.find(20);
```

Returns an iterator to one occurrence.

------------------------------------------------------------------------

## count()

``` cpp
ms.count(10);
```

Returns the frequency.

Example:

    10 10 10 20

    count(10)

    ↓

    3

------------------------------------------------------------------------

## lower_bound()

Returns first element **\>= value**.

``` cpp
ms.lower_bound(15);
```

Points to

    20

------------------------------------------------------------------------

## upper_bound()

Returns first element **\> value**.

``` cpp
ms.upper_bound(10);
```

Points to the first element after the last `10`.

------------------------------------------------------------------------

## equal_range()

``` cpp
auto p = ms.equal_range(10);
```

Equivalent to

    (lower_bound(10),
     upper_bound(10))

Useful for iterating over all duplicates.

------------------------------------------------------------------------

## size()

``` cpp
ms.size();
```

------------------------------------------------------------------------

## empty()

``` cpp
ms.empty();
```

------------------------------------------------------------------------

## clear()

``` cpp
ms.clear();
```

------------------------------------------------------------------------

# Traversing

``` cpp
for(auto x : ms)
    cout << x << " ";
```

Iterator:

``` cpp
for(auto it = ms.begin(); it != ms.end(); ++it)
    cout << *it << " ";
```

------------------------------------------------------------------------

# Complete Example

``` cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    multiset<int> ms;

    ms.insert(10);
    ms.insert(10);
    ms.insert(20);
    ms.insert(30);

    cout << ms.count(10) << endl;

    ms.erase(ms.find(10));

    cout << ms.count(10) << endl;

    for(auto x : ms)
        cout << x << " ";
}
```

Output

    2
    1
    10 20 30

------------------------------------------------------------------------

# Time Complexity

  Operation         Complexity
  ----------------- ------------------
  insert()          O(log n)
  emplace()         O(log n)
  erase(key)        O(log n + count)
  erase(iterator)   O(log n)
  find()            O(log n)
  count()           O(log n + count)
  lower_bound()     O(log n)
  upper_bound()     O(log n)
  equal_range()     O(log n)
  size()            O(1)
  empty()           O(1)

------------------------------------------------------------------------

# Set vs Multiset

  Set                      Multiset
  ------------------------ -----------------------------------
  No duplicates            Duplicates allowed
  count() = 0 or 1         count() ≥ 0
  erase(key) removes one   erase(key) removes all duplicates

------------------------------------------------------------------------

# Iterator Invalidation

-   Insertion does not invalidate existing iterators.
-   Erasing invalidates only the erased iterator.
-   `clear()` invalidates all iterators.

------------------------------------------------------------------------

# Interview Questions

## Difference between set and multiset?

A `set` stores unique values, while a `multiset` stores duplicate values
in sorted order.

------------------------------------------------------------------------

## Difference between `erase(key)` and `erase(iterator)`?

-   `erase(key)` removes **all** matching elements.
-   `erase(iterator)` removes **only one** occurrence.

------------------------------------------------------------------------

## Can a multiset be indexed?

No. It is a tree-based container and does not support random access.

------------------------------------------------------------------------

# Common Coding Problems

1.  Sliding Window Median
2.  Median Finder
3.  Running Median
4.  Meeting Rooms
5.  Maximum Overlapping Intervals
6.  Frequency Maintenance
7.  Order Statistics (with extensions)
8.  Remove Duplicates while Tracking Counts
9.  Dynamic Ranking
10. Event Simulation

------------------------------------------------------------------------

# Tips

-   Use `multiset` when duplicate values are important.
-   Prefer `erase(iterator)` when removing only one occurrence.
-   `lower_bound()`, `upper_bound()`, and `equal_range()` are extremely
    useful for handling duplicate ranges.
