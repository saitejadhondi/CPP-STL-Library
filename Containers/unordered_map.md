# C++ STL - Unordered Map (`std::unordered_map`)

> Interview-focused notes on the C++ STL Unordered Map.

------------------------------------------------------------------------

# What is an Unordered Map?

`std::unordered_map` is an associative container that stores **key-value
pairs** using a **Hash Table**.

-   Keys are **unique**
-   Elements are **not stored in sorted order**
-   Provides **average O(1)** insertion, lookup, and deletion

``` cpp
#include <unordered_map>

unordered_map<int, string> mp;
```

Example:

``` cpp
mp[2] = "Bob";
mp[1] = "Alice";
mp[3] = "Charlie";
```

Possible Output:

    2 -> Bob
    1 -> Alice
    3 -> Charlie

The iteration order is **not guaranteed**.

------------------------------------------------------------------------

# When Should You Use It?

Use `unordered_map` when:

-   Ordering is not required.
-   Fast average lookups are important.
-   Frequency counting.
-   Hash-based indexing.
-   Graph adjacency lists.
-   Caching.

Applications:

-   Two Sum
-   Word Frequency
-   Graph Algorithms
-   Memoization
-   Database Indexing

------------------------------------------------------------------------

# Internal Working

Internally it uses a **Hash Table**.

    Key
     ↓
    Hash Function
     ↓
    Bucket Number
     ↓
    Key-Value Pair Stored

If multiple keys map to the same bucket, a **collision** occurs.

------------------------------------------------------------------------

# Buckets, Load Factor & Rehashing

Useful functions:

``` cpp
mp.bucket_count();
mp.bucket(key);
mp.load_factor();
mp.rehash(100);
mp.reserve(1000);
```

Formula:

    Load Factor = size / bucket_count

When the load factor becomes large, the map performs **rehashing**,
creating more buckets.

------------------------------------------------------------------------

# Declaration

``` cpp
unordered_map<int,int> mp;
unordered_map<string,int> freq;
unordered_map<int,string> names;
```

------------------------------------------------------------------------

# Important Functions

## operator\[\]

``` cpp
mp[10] = 100;
```

If the key exists, the value is updated.

Otherwise a new key is inserted.

------------------------------------------------------------------------

## at()

``` cpp
cout << mp.at(10);
```

Throws `std::out_of_range` if the key is absent.

Does **not** insert a new key.

------------------------------------------------------------------------

## insert()

``` cpp
mp.insert({1,"Alice"});
```

If the key already exists, insertion fails.

Average Complexity:

    O(1)

------------------------------------------------------------------------

## emplace()

``` cpp
mp.emplace(2,"Bob");
```

Constructs directly in place.

------------------------------------------------------------------------

## try_emplace() (C++17)

``` cpp
mp.try_emplace(3,"Charlie");
```

Only inserts if the key does not exist.

------------------------------------------------------------------------

## erase()

``` cpp
mp.erase(1);
mp.erase(mp.begin());
```

------------------------------------------------------------------------

## find()

``` cpp
auto it = mp.find(2);

if(it != mp.end())
    cout << it->second;
```

------------------------------------------------------------------------

## count()

Returns

    0

    or

    1

------------------------------------------------------------------------

## size()

``` cpp
mp.size();
```

------------------------------------------------------------------------

## empty()

``` cpp
mp.empty();
```

------------------------------------------------------------------------

## clear()

``` cpp
mp.clear();
```

------------------------------------------------------------------------

# Traversing

Range-based loop

``` cpp
for(auto x : mp)
    cout << x.first << " " << x.second << endl;
```

Iterator

``` cpp
for(auto it = mp.begin(); it != mp.end(); ++it)
    cout << it->first << " " << it->second << endl;
```

Structured Bindings

``` cpp
for(auto &[key,value] : mp)
    cout << key << " " << value << endl;
```

Remember:

Traversal order is unpredictable.

------------------------------------------------------------------------

# Complete Example

``` cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main()
{
    unordered_map<int,string> mp;

    mp[2] = "Bob";
    mp[1] = "Alice";

    mp.emplace(3,"Charlie");

    for(auto &[k,v] : mp)
        cout << k << " -> " << v << endl;

    cout << mp.count(2) << endl;

    mp.erase(2);

    cout << mp.count(2);
}
```

------------------------------------------------------------------------

# Time Complexity

  Operation       Average   Worst
  --------------- --------- -------
  operator\[\]    O(1)      O(n)
  at()            O(1)      O(n)
  insert()        O(1)      O(n)
  emplace()       O(1)      O(n)
  try_emplace()   O(1)      O(n)
  erase()         O(1)      O(n)
  find()          O(1)      O(n)
  count()         O(1)      O(n)
  size()          O(1)      O(1)
  empty()         O(1)      O(1)

------------------------------------------------------------------------

# Map vs Unordered Map

  Map                       Unordered Map
  ------------------------- ---------------
  Red-Black Tree            Hash Table
  Sorted                    Unordered
  O(log n)                  Average O(1)
  lower_bound() available   Not available
  upper_bound() available   Not available

------------------------------------------------------------------------

# operator\[\] vs at()

  operator\[\]                      at()
  --------------------------------- ----------------------------
  Inserts missing key               Does not insert
  Updates existing value            Read-only access
  Returns default value if absent   Throws exception if absent

------------------------------------------------------------------------

# Iterator Invalidation

-   Insert may invalidate iterators if rehashing occurs.
-   Erase invalidates only erased iterator.
-   Rehash invalidates all iterators.
-   Clear invalidates all iterators.

------------------------------------------------------------------------

# Custom Hash Example

``` cpp
struct PairHash
{
    size_t operator()(const pair<int,int>& p) const
    {
        return hash<int>()(p.first) ^
               (hash<int>()(p.second)<<1);
    }
};

unordered_map<pair<int,int>, int, PairHash> mp;
```

------------------------------------------------------------------------

# Interview Questions

## Why is unordered_map faster than map?

Because hashing provides average O(1) access.

------------------------------------------------------------------------

## Why can worst-case become O(n)?

If many keys collide into the same bucket.

------------------------------------------------------------------------

## Can we use lower_bound()?

No.

Elements are unordered.

------------------------------------------------------------------------

## Why does operator\[\] insert missing keys?

It ensures every accessed key has an associated value.

------------------------------------------------------------------------

# Common Coding Problems

1.  Two Sum
2.  Group Anagrams
3.  Word Frequency
4.  Top K Frequent Elements
5.  Subarray Sum Equals K
6.  Longest Consecutive Sequence
7.  Isomorphic Strings
8.  Graph Adjacency List
9.  LRU Cache
10. Memoization

------------------------------------------------------------------------

# Tips

-   Prefer `unordered_map` for fast lookups.
-   Use `reserve()` for large datasets.
-   Never rely on iteration order.
-   Use `map` whenever sorted traversal or ordered operations are
    required.
