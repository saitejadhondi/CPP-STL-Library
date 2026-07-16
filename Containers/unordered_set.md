# C++ STL - Unordered Set (`std::unordered_set`)

> Interview-focused notes on the C++ STL Unordered Set.

------------------------------------------------------------------------

# What is an Unordered Set?

`std::unordered_set` stores **unique elements** using a **Hash Table**.

Unlike `set`:

-   No duplicate values
-   No sorted order
-   Very fast average lookup, insertion, and deletion

``` cpp
unordered_set<int> us;
```

Example:

``` cpp
us.insert(30);
us.insert(10);
us.insert(20);
us.insert(10);
```

Possible Output:

    20 30 10

The order is **not guaranteed**.

------------------------------------------------------------------------

# When to Use?

Use `unordered_set` when:

-   Ordering is **not** required.
-   Fast membership testing is needed.
-   Removing duplicates.
-   Frequency-independent lookups.

Applications:

-   Duplicate detection
-   Visited nodes in Graphs
-   BFS/DFS
-   Hash-based searching
-   Caching

------------------------------------------------------------------------

# Internal Working

`unordered_set` is implemented using a **Hash Table**.

    Hash Function

    Value

    ↓

    Bucket Number

    ↓

    Stored in Bucket

Example

    Buckets

    0 : 20

    1 :

    2 : 12 → 42

    3 : 15

    4 : 7

Two values mapping to the same bucket cause a **collision**.

------------------------------------------------------------------------

# Buckets

Each bucket stores one or more elements.

Important functions:

``` cpp
us.bucket_count();
us.bucket(x);
```

------------------------------------------------------------------------

# Load Factor

    load_factor = size / bucket_count

Higher load factor → more collisions.

``` cpp
us.load_factor();
```

------------------------------------------------------------------------

# Rehashing

When load factor becomes too high, the container allocates more buckets
and redistributes all elements.

``` cpp
us.rehash(100);
```

or

``` cpp
us.reserve(1000);
```

------------------------------------------------------------------------

# Declaration

``` cpp
#include <unordered_set>

unordered_set<int> us;
unordered_set<string> names;
unordered_set<pair<int,int>, CustomHash> pts;
```

------------------------------------------------------------------------

# Important Functions

## insert()

``` cpp
us.insert(10);
```

Average: **O(1)**

Worst: **O(n)**

------------------------------------------------------------------------

## emplace()

``` cpp
us.emplace(20);
```

Constructs object in place.

------------------------------------------------------------------------

## erase()

``` cpp
us.erase(20);
```

Average: **O(1)**

------------------------------------------------------------------------

## find()

``` cpp
auto it=us.find(30);

if(it!=us.end())
    cout<<"Found";
```

Average: **O(1)**

------------------------------------------------------------------------

## count()

Returns

    0

    or

    1

``` cpp
us.count(10);
```

------------------------------------------------------------------------

## size()

``` cpp
us.size();
```

------------------------------------------------------------------------

## empty()

``` cpp
us.empty();
```

------------------------------------------------------------------------

## clear()

``` cpp
us.clear();
```

------------------------------------------------------------------------

# Traversing

``` cpp
for(auto x:us)
    cout<<x<<" ";
```

or

``` cpp
for(auto it=us.begin();it!=us.end();it++)
    cout<<*it<<" ";
```

Remember:

Iteration order is unpredictable.

------------------------------------------------------------------------

# Complete Example

``` cpp
#include<iostream>
#include<unordered_set>
using namespace std;

int main()
{
    unordered_set<int> us;

    us.insert(20);
    us.insert(10);
    us.insert(30);
    us.insert(20);

    for(auto x:us)
        cout<<x<<" ";

    cout<<endl;

    us.erase(20);

    cout<<us.count(20)<<endl;

    if(us.find(10)!=us.end())
        cout<<"Found";
}
```

------------------------------------------------------------------------

# Time Complexity

  Operation   Average   Worst
  ----------- --------- -------
  insert()    O(1)      O(n)
  emplace()   O(1)      O(n)
  erase()     O(1)      O(n)
  find()      O(1)      O(n)
  count()     O(1)      O(n)
  size()      O(1)      O(1)
  empty()     O(1)      O(1)

------------------------------------------------------------------------

# Set vs Unordered Set

  Set              Unordered Set
  ---------------- ---------------
  Red-Black Tree   Hash Table
  Sorted           Unordered
  O(log n)         Avg O(1)
  lower_bound()    Not Supported
  upper_bound()    Not Supported

------------------------------------------------------------------------

# Iterator Invalidation

-   Insert may invalidate iterators if rehashing occurs.
-   Erase invalidates only erased iterator.
-   Rehash invalidates all iterators.

------------------------------------------------------------------------

# Custom Hash

``` cpp
struct PairHash
{
    size_t operator()(const pair<int,int>& p) const
    {
        return hash<int>()(p.first) ^
               (hash<int>()(p.second)<<1);
    }
};

unordered_set<pair<int,int>, PairHash> us;
```

------------------------------------------------------------------------

# Interview Questions

## Why is average complexity O(1)?

Because hashing directly maps keys to buckets.

------------------------------------------------------------------------

## Why worst-case O(n)?

If many keys collide into the same bucket.

------------------------------------------------------------------------

## Can we use lower_bound()?

No.

Elements are not stored in sorted order.

------------------------------------------------------------------------

## Why doesn't it allow duplicates?

Like `set`, every key must be unique.

------------------------------------------------------------------------

# Common Coding Problems

1.  Contains Duplicate
2.  Longest Consecutive Sequence
3.  Happy Number
4.  Intersection of Arrays
5.  Unique Email Addresses
6.  Word Break
7.  Graph Traversal (Visited Set)
8.  Sudoku Validation
9.  Distinct Islands
10. Remove Duplicates

------------------------------------------------------------------------

# Tips

-   Prefer `unordered_set` over `set` when ordering is unnecessary.
-   Use `reserve()` to reduce rehashing for large datasets.
-   Avoid depending on iteration order.
-   Great for fast lookups in interviews.
