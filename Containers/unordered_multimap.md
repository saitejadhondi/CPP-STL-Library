# C++ STL - Unordered Multimap (`std::unordered_multimap`)

> Interview-focused notes on the C++ STL Unordered Multimap.

------------------------------------------------------------------------

# What is an Unordered Multimap?

`std::unordered_multimap` is a hash table-based associative container
that stores **key-value pairs**, where **multiple values can have the
same key**.

Features:

-   Duplicate keys are allowed.
-   Keys are **not sorted**.
-   Average **O(1)** insertion, lookup, and deletion.
-   Implemented internally using a **Hash Table**.

``` cpp
#include <unordered_map>

unordered_multimap<int, string> umm;
```

Example:

``` cpp
umm.insert({1,"Alice"});
umm.insert({1,"Alex"});
umm.insert({2,"Bob"});
```

Possible Output:

    2 -> Bob
    1 -> Alice
    1 -> Alex

The order is **not guaranteed**.

------------------------------------------------------------------------

# When Should You Use It?

Use `unordered_multimap` when:

-   One key maps to multiple values.
-   Ordering does not matter.
-   Fast average lookup is required.

Applications:

-   Search Indexes
-   Student → Subjects
-   Product → Reviews
-   Web Server Logs
-   Graphs with Parallel Edges
-   Event Collection

------------------------------------------------------------------------

# Internal Working

`unordered_multimap` uses a **Hash Table**.

    Key
     ↓
    Hash Function
     ↓
    Bucket Number
     ↓
    Store Key-Value Pair

Multiple entries with the same key can exist in the same bucket.

If different keys hash to the same bucket, a **collision** occurs.

------------------------------------------------------------------------

# Buckets, Load Factor & Rehashing

Useful member functions:

``` cpp
umm.bucket_count();
umm.bucket(key);
umm.load_factor();
umm.rehash(100);
umm.reserve(1000);
```

Formula:

    Load Factor = size / bucket_count

Higher load factor increases collisions.

------------------------------------------------------------------------

# Declaration

``` cpp
unordered_multimap<int,string> umm;
unordered_multimap<string,int> freq;
```

------------------------------------------------------------------------

# Important Functions

## insert()

``` cpp
umm.insert({1,"Alice"});
umm.insert({1,"Alex"});
```

Duplicate keys are allowed.

Average Complexity: **O(1)**

Worst Case: **O(n)**

------------------------------------------------------------------------

## emplace()

``` cpp
umm.emplace(2,"Bob");
```

Constructs element directly.

------------------------------------------------------------------------

## erase(key)

``` cpp
umm.erase(1);
```

Removes **all** key-value pairs having key `1`.

------------------------------------------------------------------------

## erase(iterator)

``` cpp
auto it = umm.find(1);

umm.erase(it);
```

Removes **one occurrence**.

------------------------------------------------------------------------

## find()

``` cpp
auto it = umm.find(2);

if(it != umm.end())
    cout << it->second;
```

Returns one matching element.

------------------------------------------------------------------------

## count()

``` cpp
umm.count(1);
```

Returns the number of values associated with the key.

------------------------------------------------------------------------

## equal_range()

``` cpp
auto range = umm.equal_range(1);

for(auto it = range.first; it != range.second; ++it)
    cout << it->second << endl;
```

Best way to iterate all duplicate keys.

------------------------------------------------------------------------

## size()

``` cpp
umm.size();
```

------------------------------------------------------------------------

## empty()

``` cpp
umm.empty();
```

------------------------------------------------------------------------

## clear()

``` cpp
umm.clear();
```

------------------------------------------------------------------------

# Traversing

``` cpp
for(auto &[key,value] : umm)
    cout << key << " -> " << value << endl;
```

or

``` cpp
for(auto it = umm.begin(); it != umm.end(); ++it)
    cout << it->first << " " << it->second << endl;
```

Remember:

Iteration order is unpredictable.

------------------------------------------------------------------------

# Complete Example

``` cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main()
{
    unordered_multimap<int,string> umm;

    umm.insert({1,"Alice"});
    umm.insert({1,"Alex"});
    umm.emplace(2,"Bob");

    cout << umm.count(1) << endl;

    auto range = umm.equal_range(1);

    for(auto it = range.first; it != range.second; ++it)
        cout << it->second << " ";

    umm.erase(umm.find(1));

    cout << endl;
    cout << umm.count(1);
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
  equal_range()     O(count)   O(n)
  size()            O(1)       O(1)
  empty()           O(1)       O(1)

------------------------------------------------------------------------

# Multimap vs Unordered Multimap

  Multimap                  Unordered Multimap
  ------------------------- --------------------
  Red-Black Tree            Hash Table
  Ordered                   Unordered
  O(log n)                  Average O(1)
  lower_bound() supported   Not supported
  upper_bound() supported   Not supported

------------------------------------------------------------------------

# Iterator Invalidation

-   Insert may invalidate iterators if rehashing occurs.
-   Erase invalidates only erased iterator.
-   Rehash invalidates all iterators.
-   Clear invalidates all iterators.

------------------------------------------------------------------------

# Interview Questions

## Difference between multimap and unordered_multimap?

-   `multimap` keeps keys sorted.
-   `unordered_multimap` provides faster average lookup but does not
    preserve order.

------------------------------------------------------------------------

## Why is operator\[\] unavailable?

Duplicate keys make it impossible to uniquely identify a single value.

------------------------------------------------------------------------

## Best way to access all values for a key?

Use:

``` cpp
equal_range(key)
```

------------------------------------------------------------------------

## Why can worst-case complexity become O(n)?

Because many keys may hash into the same bucket, causing collisions.

------------------------------------------------------------------------

# Common Coding Problems

1.  Student → Multiple Subjects
2.  Product → Multiple Reviews
3.  Group Records by Key
4.  Search Engine Index
5.  Log Aggregation
6.  Parallel Graph Edges
7.  Duplicate Event Processing
8.  Recommendation Systems

------------------------------------------------------------------------

# Tips

-   Use `unordered_multimap` when duplicate keys are required but
    ordering is not.
-   Prefer `reserve()` for large datasets.
-   Never rely on traversal order.
-   Use `equal_range()` to efficiently iterate over all values for a
    key.
