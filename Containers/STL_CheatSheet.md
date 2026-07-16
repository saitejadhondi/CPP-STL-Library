# C++ STL Cheat Sheet

> Quick revision notes for coding interviews.

------------------------------------------------------------------------

# Sequence Containers

  ----------------------------------------------------------------------------
  Container      Ordered   Duplicates   Access   Insert/Delete   Internal DS
  -------------- --------- ------------ -------- --------------- -------------
  vector         Yes       Yes          O(1)     End: O(1)\*     Dynamic Array

  deque          Yes       Yes          O(1)     Front/Back:     Block Array
                                                 O(1)            

  list           Yes       Yes          O(n)     O(1)            Doubly Linked
                                                                 List

  forward_list   Yes       Yes          O(n)     O(1)            Singly Linked
                                                                 List
  ----------------------------------------------------------------------------

\* Amortized.

------------------------------------------------------------------------

# Container Adaptors

  Container        Order              Top Access
  ---------------- ------------------ ------------
  stack            LIFO               top()
  queue            FIFO               front()
  priority_queue   Highest Priority   top()

------------------------------------------------------------------------

# Associative Containers

  Container   Ordered   Duplicate Keys   Complexity   Internal DS
  ----------- --------- ---------------- ------------ ----------------
  set         ✓         ✗                O(log n)     Red-Black Tree
  multiset    ✓         ✓                O(log n)     Red-Black Tree
  map         ✓         ✗                O(log n)     Red-Black Tree
  multimap    ✓         ✓                O(log n)     Red-Black Tree

------------------------------------------------------------------------

# Unordered Associative Containers

  Container            Ordered   Duplicate Keys   Avg    Worst   Internal DS
  -------------------- --------- ---------------- ------ ------- -------------
  unordered_set        ✗         ✗                O(1)   O(n)    Hash Table
  unordered_multiset   ✗         ✓                O(1)   O(n)    Hash Table
  unordered_map        ✗         ✗                O(1)   O(n)    Hash Table
  unordered_multimap   ✗         ✓                O(1)   O(n)    Hash Table

------------------------------------------------------------------------

# Most Used Functions

## Vector

``` cpp
push_back()
emplace_back()
pop_back()
front()
back()
at()
insert()
erase()
clear()
size()
empty()
```

## Stack

``` cpp
push()
pop()
top()
size()
empty()
```

## Queue

``` cpp
push()
pop()
front()
back()
size()
empty()
```

## Priority Queue

``` cpp
push()
pop()
top()
```

## Set / Multiset

``` cpp
insert()
emplace()
erase()
find()
count()
lower_bound()
upper_bound()
equal_range()
```

## Map / Multimap

``` cpp
operator[]
at()
insert()
emplace()
try_emplace()
erase()
find()
count()
lower_bound()
upper_bound()
equal_range()
```

## Unordered Containers

``` cpp
insert()
emplace()
erase()
find()
count()
bucket_count()
bucket()
load_factor()
rehash()
reserve()
```

------------------------------------------------------------------------

# Important STL Algorithms

``` cpp
sort(begin,end);
reverse(begin,end);
find(begin,end,x);
count(begin,end,x);
binary_search(begin,end,x);
lower_bound(begin,end,x);
upper_bound(begin,end,x);
min_element(begin,end);
max_element(begin,end);
accumulate(begin,end,0);
next_permutation(begin,end);
prev_permutation(begin,end);
```

------------------------------------------------------------------------

# Complexity Cheat Sheet

  --------------------------------------------------------------------------------------------
  Operation    vector   deque   stack     queue      priority_queue   set/map   unordered\_\*
  ----------- -------- ------- ------- ------------ ---------------- --------- ---------------
  Access        O(1)    O(1)     Top    Front/Back        Top        O(log n)     O(1) avg

  Insert        End     Ends    O(1)       O(1)         O(log n)     O(log n)     O(1) avg
               O(1)\*   O(1)                                                   

  Delete      End O(1)  Ends    O(1)       O(1)         O(log n)     O(log n)     O(1) avg
                        O(1)                                                   

  Search        O(n)    O(n)    O(n)       O(n)           O(n)       O(log n)     O(1) avg
  --------------------------------------------------------------------------------------------

------------------------------------------------------------------------

# Frequently Asked Interview Questions

-   `vector` vs `deque`
-   `set` vs `unordered_set`
-   `map` vs `unordered_map`
-   `push_back()` vs `emplace_back()`
-   `insert()` vs `emplace()`
-   `operator[]` vs `at()`
-   `erase(key)` vs `erase(iterator)`
-   `lower_bound()` vs `upper_bound()`
-   Why is `unordered_map` average O(1)?
-   Why is `priority_queue` implemented using a heap?
-   Why can't `set` be indexed?
-   Why is `push_back()` amortized O(1)?

------------------------------------------------------------------------

# Which Container Should I Use?

  Requirement                    Best Choice
  ------------------------------ --------------------
  Dynamic Array                  vector
  Insert/Delete at Both Ends     deque
  LIFO                           stack
  FIFO                           queue
  Highest Priority               priority_queue
  Unique + Ordered               set
  Unique + Fast Lookup           unordered_set
  Duplicate + Ordered            multiset
  Key-Value + Ordered            map
  Key-Value + Fast Lookup        unordered_map
  Duplicate Keys + Ordered       multimap
  Duplicate Keys + Fast Lookup   unordered_multimap

------------------------------------------------------------------------

# STL Headers

``` cpp
#include <vector>
#include <deque>
#include <stack>
#include <queue>
#include <set>
#include <unordered_set>
#include <map>
#include <unordered_map>
#include <algorithm>
#include <numeric>
#include <utility>
#include <iterator>
#include <functional>
```

------------------------------------------------------------------------

# Interview Tip

-   Ordered → `set` / `map`
-   Fast lookup → `unordered_set` / `unordered_map`
-   Duplicates → `multiset` / `multimap`
-   Top element → `priority_queue`
-   Dynamic array → `vector`
-   Sliding window → `deque`
-   Graph shortest path → `priority_queue`
-   Frequency counting → `unordered_map`
