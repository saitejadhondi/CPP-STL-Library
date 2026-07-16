# C++ STL - Unordered Multiset (`std::unordered_multiset`)

> Interview-focused notes on the C++ STL Unordered Multiset.

------------------------------------------------------------------------

## Learning path

- Previous: [Multiset](multiset.md)
- Next: [Map](map.md)
- Related: [Unordered Set](unordered_set.md), [Unordered Map](unordered_map.md)

------------------------------------------------------------------------

# What is an Unordered Multiset?

`std::unordered_multiset` is a hash-table based associative container
that:

-   Allows **duplicate elements**
-   Does **not** maintain sorted order
-   Provides **average O(1)** insertion, deletion, and lookup

``` cpp
#include <unordered_set>

unordered_multiset<int> ums;
```

Example:

``` cpp
ums.insert(10);
ums.insert(10);
ums.insert(20);
ums.insert(5);
```

Possible Output:

    20 10 5 10

The order is **not guaranteed**.

------------------------------------------------------------------------

# When Should You Use It?

Use `unordered_multiset` when:

-   Duplicate values are important.
-   Ordering does not matter.
-   Fast average lookup is required.

Applications:

-   Frequency-based algorithms
-   Duplicate tracking
-   Streaming data
-   Sliding window problems
-   Event logging

------------------------------------------------------------------------

# Internal Working

Internally it uses a **Hash Table**.

    Hash Function
          ↓
     Bucket Number
          ↓
     Store Element

Multiple duplicate values may exist in the same bucket.

When many keys map to one bucket, a **collision** occurs.

------------------------------------------------------------------------

# Buckets, Load Factor & Rehashing

Useful functions:

``` cpp
ums.bucket_count();
ums.bucket(value);
ums.load_factor();
ums.rehash(100);
ums.reserve(1000);
```

Load Factor:

    load_factor = size / bucket_count

Higher load factor ⇒ more collisions.

------------------------------------------------------------------------

# Declaration

``` cpp
unordered_multiset<int> ums;
unordered_multiset<string> words;
```

------------------------------------------------------------------------

# Important Functions

## insert()

``` cpp
ums.insert(10);
ums.insert(10);
```

Average: **O(1)**

Worst: **O(n)**

------------------------------------------------------------------------

## emplace()

``` cpp
ums.emplace(20);
```

Constructs the object directly.

------------------------------------------------------------------------

## erase(key)

Removes **all occurrences**.

``` cpp
ums.erase(10);
```

    10 10 10 20

    ↓

    20

------------------------------------------------------------------------

## erase(iterator)

Removes only one occurrence.

``` cpp
auto it = ums.find(10);

ums.erase(it);
```

    10 10 10 20

    ↓

    10 10 20

------------------------------------------------------------------------

## find()

``` cpp
auto it = ums.find(20);
```

Returns an iterator to one matching element.

------------------------------------------------------------------------

## count()

``` cpp
cout << ums.count(10);
```

Returns the frequency.

------------------------------------------------------------------------

## size()

``` cpp
ums.size();
```

------------------------------------------------------------------------

## empty()

``` cpp
ums.empty();
```

------------------------------------------------------------------------

## clear()

``` cpp
ums.clear();
```

------------------------------------------------------------------------

# Traversing

``` cpp
for(auto x : ums)
    cout << x << " ";
```

or

``` cpp
for(auto it = ums.begin(); it != ums.end(); ++it)
    cout << *it << " ";
```

Remember:

Iteration order is unpredictable.

------------------------------------------------------------------------

# Complete Example

``` cpp
#include <iostream>
#include <unordered_set>
using namespace std;

int main()
{
    unordered_multiset<int> ums;

    ums.insert(10);
    ums.insert(10);
    ums.insert(20);
    ums.insert(30);

    cout << ums.count(10) << endl;

    ums.erase(ums.find(10));

    cout << ums.count(10) << endl;

    for(auto x : ums)
        cout << x << " ";
}
```

------------------------------------------------------------------------

# Time Complexity

  Operation         Average    Worst
  ----------------- ---------- -------
  insert()          O(1)       O(n)
  emplace()         O(1)       O(n)
  erase(key)        O(count)   O(n)
  erase(iterator)   O(1)       O(n)
  find()            O(1)       O(n)
  count()           O(count)   O(n)
  size()            O(1)       O(1)
  empty()           O(1)       O(1)

------------------------------------------------------------------------

# Multiset vs Unordered Multiset

  Multiset                  Unordered Multiset
  ------------------------- --------------------
  Red-Black Tree            Hash Table
  Sorted                    Unordered
  O(log n)                  Avg O(1)
  lower_bound() available   Not available
  upper_bound() available   Not available

------------------------------------------------------------------------

# Iterator Invalidation

-   Insert may invalidate iterators if rehashing occurs.
-   Erasing invalidates only erased iterator.
-   Rehash invalidates all iterators.
-   Clear invalidates all iterators.

------------------------------------------------------------------------

# Interview Questions

## Difference between multiset and unordered_multiset?

-   `multiset` keeps elements sorted.
-   `unordered_multiset` provides faster average operations but no
    ordering.

------------------------------------------------------------------------

## Why is the average complexity O(1)?

Hashing maps values directly to buckets.

------------------------------------------------------------------------

## Why is the worst-case complexity O(n)?

Many collisions can place all elements into the same bucket.

------------------------------------------------------------------------

## Can we use lower_bound() or upper_bound()?

No. The container is unordered.

------------------------------------------------------------------------

# Common Coding Problems

1.  Frequency Counting
2.  Sliding Window Frequency
3.  Duplicate Detection
4.  Grouping Equal Values
5.  Log/Event Analysis
6.  Inventory Tracking
7.  Word Frequency
8.  Data Stream Processing
9.  Remove Duplicates with Counts
10. Hash-based Simulations

------------------------------------------------------------------------

# Tips

-   Use `unordered_multiset` when duplicates matter but ordering does
    not.
-   Use `reserve()` for large datasets to reduce rehashing.
-   Never depend on iteration order.
-   Prefer `multiset` if ordered traversal or `lower_bound()` is
    required.
