# C++ STL - Multimap (`std::multimap`)

> Interview-focused notes on the C++ STL Multimap.

------------------------------------------------------------------------

## Learning path

- Previous: [Unordered Map](unordered_map.md)
- Next: [Unordered Multimap](unordered_multimap.md)
- Related: [Map](map.md), [Multiset](multiset.md)

------------------------------------------------------------------------

# What is a Multimap?

A **multimap** is an ordered associative container that stores
**key-value pairs** where **multiple values can share the same key**.

-   Duplicate keys are allowed.
-   Keys are automatically stored in ascending order.
-   Implemented using a **Red-Black Tree**.

``` cpp
#include <map>

multimap<int,string> mm;
```

Example:

``` cpp
mm.insert({1,"Alice"});
mm.insert({1,"Alex"});
mm.insert({2,"Bob"});
```

Output:

    1 -> Alice
    1 -> Alex
    2 -> Bob

------------------------------------------------------------------------

# When Should You Use It?

Use `multimap` when:

-   One key maps to multiple values.
-   Ordering by key is required.
-   Efficient searching of duplicate keys is needed.

Applications:

-   Student → Multiple Courses
-   Employee → Multiple Projects
-   Event Scheduling
-   Grouped Records
-   Phone Directory

------------------------------------------------------------------------

# Internal Working

`multimap` is implemented using a **Red-Black Tree**.

Properties:

-   Self-balancing BST
-   Ordered traversal
-   Duplicate keys supported
-   Operations in **O(log n)**

------------------------------------------------------------------------

# Declaration

``` cpp
multimap<int,string> mm;
multimap<string,int> words;
multimap<int,int,greater<int>> rev;
```

------------------------------------------------------------------------

# Important Functions

## insert()

``` cpp
mm.insert({1,"Alice"});
mm.insert({1,"Alex"});
```

Duplicates are allowed.

Complexity: **O(log n)**

------------------------------------------------------------------------

## emplace()

``` cpp
mm.emplace(2,"Bob");
```

Constructs the element in place.

------------------------------------------------------------------------

## erase(key)

``` cpp
mm.erase(1);
```

Removes **all** entries having key `1`.

------------------------------------------------------------------------

## erase(iterator)

``` cpp
auto it = mm.find(1);
mm.erase(it);
```

Removes **one occurrence**.

------------------------------------------------------------------------

## find()

``` cpp
auto it = mm.find(1);
```

Returns an iterator to the first matching key.

------------------------------------------------------------------------

## count()

``` cpp
mm.count(1);
```

Returns the number of values associated with the key.

------------------------------------------------------------------------

## lower_bound()

Returns first element whose key is **\>=** the given key.

------------------------------------------------------------------------

## upper_bound()

Returns first element whose key is **\>** the given key.

------------------------------------------------------------------------

## equal_range()

``` cpp
auto range = mm.equal_range(1);

for(auto it=range.first; it!=range.second; ++it)
    cout<<it->first<<" "<<it->second<<endl;
```

The best way to iterate over all values for one key.

------------------------------------------------------------------------

## size(), empty(), clear()

``` cpp
mm.size();
mm.empty();
mm.clear();
```

------------------------------------------------------------------------

# Traversing

``` cpp
for(auto &[key,value] : mm)
    cout<<key<<" -> "<<value<<endl;
```

Or

``` cpp
for(auto it=mm.begin(); it!=mm.end(); ++it)
    cout<<it->first<<" "<<it->second<<endl;
```

------------------------------------------------------------------------

# Complete Example

``` cpp
#include<iostream>
#include<map>
using namespace std;

int main()
{
    multimap<int,string> mm;

    mm.insert({1,"Alice"});
    mm.insert({1,"Alex"});
    mm.emplace(2,"Bob");

    cout<<mm.count(1)<<endl;

    auto range = mm.equal_range(1);

    for(auto it=range.first; it!=range.second; ++it)
        cout<<it->second<<" ";

    mm.erase(mm.find(1));

    cout<<"\n"<<mm.count(1);
}
```

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

# Map vs Multimap

  Map                              Multimap
  -------------------------------- -------------------------------
  Unique keys                      Duplicate keys allowed
  count() is 0 or 1                count() can be \>1
  insert() ignores duplicate key   insert() stores duplicate key

------------------------------------------------------------------------

# Iterator Invalidation

-   Insertion does not invalidate existing iterators.
-   Erasing invalidates only erased iterator.
-   `clear()` invalidates all iterators.

------------------------------------------------------------------------

# Interview Questions

## Difference between map and multimap?

`map` stores unique keys, while `multimap` allows multiple values for
the same key.

## Why is operator\[\] unavailable?

Because duplicate keys exist, there is no unique value to return.

## Best way to iterate all duplicate keys?

Use `equal_range()`.

------------------------------------------------------------------------

# Common Coding Problems

1.  Group Students by Marks
2.  Employee Project Mapping
3.  Interval Grouping
4.  Event Scheduling
5.  Contact Book with Multiple Numbers
6.  Duplicate Key Processing
7.  Group Records by Category
8.  Log Aggregation

------------------------------------------------------------------------

# Tips

-   Use `multimap` when one key can have many values.
-   Prefer `equal_range()` over repeated `find()`.
-   Remember that `operator[]` is **not supported**.
