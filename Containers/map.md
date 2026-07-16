# C++ STL - Map (`std::map`)

> Interview-focused notes on the C++ STL Map.

------------------------------------------------------------------------

# What is a Map?

A **map** is an ordered associative container that stores **key-value
pairs**.

-   Keys are **unique**.
-   Keys are automatically stored in **sorted order**.
-   Implemented internally using a **Red-Black Tree**.

``` cpp
map<int,string> mp;

mp[1] = "Alice";
mp[3] = "Charlie";
mp[2] = "Bob";
```

Output (ordered by key):

    1 -> Alice
    2 -> Bob
    3 -> Charlie

------------------------------------------------------------------------

# When to Use?

Use a map when you need:

-   Key → Value mapping
-   Automatic sorting by key
-   Fast lookup, insertion and deletion
-   Ordered traversal

Applications:

-   Frequency counting
-   Dictionaries
-   Caching metadata
-   Employee ID → Details
-   Configuration storage

------------------------------------------------------------------------

# Internal Working

`std::map` uses a **Red-Black Tree**.

Properties:

-   Self-balancing BST
-   Height ≈ log₂(n)
-   Ordered traversal
-   All major operations: **O(log n)**

------------------------------------------------------------------------

# Declaration

``` cpp
#include <map>

map<int,int> mp;
map<string,int> freq;
map<int,string> names;

// Descending order
map<int,string,greater<int>> rev;
```

------------------------------------------------------------------------

# Important Functions

## operator\[\]

``` cpp
mp[10] = 100;
```

If the key exists, its value is updated.

If the key does not exist, it is inserted.

------------------------------------------------------------------------

## at()

``` cpp
cout << mp.at(10);
```

Unlike `operator[]`, `at()` **does not create** a new key.

It throws `std::out_of_range` if the key is absent.

------------------------------------------------------------------------

## insert()

``` cpp
mp.insert({1,"Alice"});
mp.insert(make_pair(2,"Bob"));
```

If the key already exists, insertion fails.

Time Complexity: **O(log n)**

------------------------------------------------------------------------

## emplace()

``` cpp
mp.emplace(3,"Charlie");
```

Constructs the element directly in place.

------------------------------------------------------------------------

## try_emplace() (C++17)

``` cpp
mp.try_emplace(4,"David");
```

Inserts only if the key is absent.

------------------------------------------------------------------------

## erase()

``` cpp
mp.erase(2);              // erase by key
mp.erase(mp.begin());     // erase by iterator
```

------------------------------------------------------------------------

## find()

``` cpp
auto it = mp.find(3);

if(it != mp.end())
    cout << it->second;
```

------------------------------------------------------------------------

## count()

Returns `0` or `1`.

``` cpp
mp.count(3);
```

------------------------------------------------------------------------

## lower_bound()

Returns first key **\>= value**.

``` cpp
mp.lower_bound(5);
```

------------------------------------------------------------------------

## upper_bound()

Returns first key **\> value**.

``` cpp
mp.upper_bound(5);
```

------------------------------------------------------------------------

## equal_range()

Returns:

    (lower_bound(key), upper_bound(key))

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

## Range-based loop

``` cpp
for(auto x : mp)
    cout << x.first << " " << x.second << endl;
```

## Iterator

``` cpp
for(auto it = mp.begin(); it != mp.end(); ++it)
    cout << it->first << " " << it->second << endl;
```

## Structured Bindings (C++17)

``` cpp
for(auto &[key,value] : mp)
    cout << key << " " << value << endl;
```

------------------------------------------------------------------------

# Complete Example

``` cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    map<int,string> mp;

    mp[2]="Bob";
    mp[1]="Alice";

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

  Operation       Complexity
  --------------- ------------
  operator\[\]    O(log n)
  at()            O(log n)
  insert()        O(log n)
  emplace()       O(log n)
  try_emplace()   O(log n)
  erase()         O(log n)
  find()          O(log n)
  count()         O(log n)
  lower_bound()   O(log n)
  upper_bound()   O(log n)
  size()          O(1)
  empty()         O(1)

------------------------------------------------------------------------

# operator\[\] vs at()

  operator\[\]                      at()
  --------------------------------- ----------------------------
  Inserts missing key               Does not insert
  Returns default value if absent   Throws exception if absent
  Useful for updates                Useful for safe reads

------------------------------------------------------------------------

# Map vs Unordered Map

  Map                       Unordered Map
  ------------------------- ---------------
  Ordered                   Unordered
  Red-Black Tree            Hash Table
  O(log n)                  Average O(1)
  lower_bound() supported   Not supported

------------------------------------------------------------------------

# Iterator Invalidation

-   Insert does **not** invalidate existing iterators.
-   Erase invalidates only the erased iterator.
-   Clear invalidates all iterators.

------------------------------------------------------------------------

# Interview Questions

## Why are keys unique?

A map models a dictionary where each key identifies exactly one value.

------------------------------------------------------------------------

## Difference between insert() and operator\[\]?

-   `insert()` never overwrites an existing key.
-   `operator[]` inserts or updates the key.

------------------------------------------------------------------------

## When should at() be preferred?

When you only want to read an existing value and avoid accidental
insertion.

------------------------------------------------------------------------

# Common Coding Problems

1.  Two Sum
2.  Group Anagrams
3.  Frequency Counter
4.  Top K Frequent Elements
5.  Vertical Order Traversal
6.  Employee Database
7.  Word Frequency
8.  Calendar Booking
9.  LRU Cache foundations
10. Ordered Event Processing

------------------------------------------------------------------------

# Tips

-   Prefer `map` when key ordering matters.
-   Prefer `unordered_map` for faster average lookups.
-   Use structured bindings (`auto &[k,v]`) for cleaner iteration.
-   Be careful: `operator[]` inserts missing keys automatically.
