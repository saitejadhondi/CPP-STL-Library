# C++ STL - Set (`std::set`)

> Interview-focused notes on the C++ STL Set.

------------------------------------------------------------------------

# What is a Set?

A **Set** is an ordered associative container that stores **unique
elements**.

-   Duplicate values are **not allowed**.
-   Elements are automatically stored in **sorted (ascending) order**.
-   Implemented internally using a **Red-Black Tree** (Self-Balancing
    Binary Search Tree).

Example:

``` cpp
set<int> st;

st.insert(30);
st.insert(10);
st.insert(20);
st.insert(10);
```

Output:

    10 20 30

Notice that: - Elements are sorted. - Duplicate `10` is ignored.

------------------------------------------------------------------------

# Why Use a Set?

Use a set when you need: - Unique elements - Automatic sorting - Fast
search, insertion, and deletion

Common use cases: - Remove duplicates - Maintain sorted data -
Membership checking - Scheduling systems - Leaderboards - Ordered lookup

------------------------------------------------------------------------

# Internal Working (Red-Black Tree)

A set is implemented using a **Red-Black Tree**.

Properties: - Self-balancing BST - Height is approximately `log₂(n)` -
Ensures all operations remain **O(log n)**

Example:

            20(B)
           /     \
        10(R)   30(R)

Whenever insertion or deletion makes the tree unbalanced, rotations and
recoloring restore balance.

------------------------------------------------------------------------

# Declaration

``` cpp
#include <set>

set<int> st;
set<string> names;
set<pair<int,int>> points;
```

Descending order:

``` cpp
set<int, greater<int>> st;
```

------------------------------------------------------------------------

# Important Functions

## insert()

``` cpp
st.insert(10);
st.insert(20);
st.insert(10);
```

Output:

    10 20

Time Complexity:

    O(log n)

------------------------------------------------------------------------

## emplace()

Constructs the object directly.

``` cpp
st.emplace(30);
```

Slightly more efficient for complex objects.

------------------------------------------------------------------------

## erase()

Erase by value:

``` cpp
st.erase(20);
```

Erase by iterator:

``` cpp
st.erase(st.begin());
```

Time Complexity:

    O(log n)

------------------------------------------------------------------------

## find()

``` cpp
auto it = st.find(10);

if(it != st.end())
    cout<<"Found";
```

Returns an iterator.

Time Complexity:

    O(log n)

------------------------------------------------------------------------

## count()

Returns either:

    0

or

    1

because duplicates are not allowed.

``` cpp
st.count(10);
```

------------------------------------------------------------------------

## size()

``` cpp
st.size();
```

------------------------------------------------------------------------

## empty()

``` cpp
st.empty();
```

------------------------------------------------------------------------

## clear()

``` cpp
st.clear();
```

Removes all elements.

------------------------------------------------------------------------

# lower_bound()

Returns the first element **greater than or equal to** the given value.

``` cpp
set<int> st={10,20,30,40};

auto it=st.lower_bound(25);
```

Points to

    30

------------------------------------------------------------------------

# upper_bound()

Returns the first element **strictly greater** than the given value.

``` cpp
auto it=st.upper_bound(20);
```

Points to

    30

------------------------------------------------------------------------

# equal_range()

Returns

    (lower_bound,
     upper_bound)

Useful in multisets and maps.

------------------------------------------------------------------------

# Traversing a Set

## Range-based loop

``` cpp
for(auto x:st)
    cout<<x<<" ";
```

------------------------------------------------------------------------

## Iterator

``` cpp
for(auto it=st.begin();it!=st.end();it++)
    cout<<*it<<" ";
```

------------------------------------------------------------------------

## Reverse Iterator

``` cpp
for(auto it=st.rbegin();it!=st.rend();it++)
    cout<<*it<<" ";
```

------------------------------------------------------------------------

# Complete Example

``` cpp
#include<iostream>
#include<set>

using namespace std;

int main()
{
    set<int> st;

    st.insert(20);
    st.insert(10);
    st.insert(40);
    st.insert(30);
    st.insert(20);

    for(auto x:st)
        cout<<x<<" ";

    cout<<endl;

    st.erase(20);

    for(auto x:st)
        cout<<x<<" ";

    return 0;
}
```

Output

    10 20 30 40

    10 30 40

------------------------------------------------------------------------

# Time Complexity

  Operation       Complexity
  --------------- ------------
  insert()        O(log n)
  emplace()       O(log n)
  erase()         O(log n)
  find()          O(log n)
  count()         O(log n)
  lower_bound()   O(log n)
  upper_bound()   O(log n)
  size()          O(1)
  empty()         O(1)

------------------------------------------------------------------------

# Vector vs Set

  Vector                     Set
  -------------------------- ----------------------
  Allows duplicates          Unique only
  Not sorted automatically   Automatically sorted
  O(1) access                No indexing
  Search O(n)                Search O(log n)

------------------------------------------------------------------------

# Set vs Unordered Set

  Set                      Unordered Set
  ------------------------ ---------------
  Sorted                   Unsorted
  Red-Black Tree           Hash Table
  O(log n)                 Average O(1)
  Supports lower_bound()   Not supported

------------------------------------------------------------------------

# Iterator Invalidation

-   Insert: Existing iterators remain valid.
-   Erase: Only erased iterator becomes invalid.
-   Clear: All iterators become invalid.

------------------------------------------------------------------------

# Interview Questions

## Why doesn't a set allow duplicates?

A set is designed to represent a mathematical set where every element is
unique.

------------------------------------------------------------------------

## Why is insertion O(log n)?

Because the Red-Black Tree remains balanced, giving a height of
approximately `log₂(n)`.

------------------------------------------------------------------------

## Why can't we use indexing?

A set is a tree, not an array. Nodes are connected by pointers, so
random access by index is not supported.

------------------------------------------------------------------------

## Difference between insert() and emplace()

-   `insert()` inserts an existing object.
-   `emplace()` constructs the object directly inside the container.

------------------------------------------------------------------------

# Common Coding Problems

1.  Remove Duplicates
2.  Longest Consecutive Sequence
3.  Contains Duplicate
4.  K Empty Slots
5.  Ordered Stream
6.  Design Leaderboard
7.  Skyline Problem
8.  Count Distinct Elements
9.  Sliding Window Distinct Count
10. Employee Free Time

------------------------------------------------------------------------

# Tips

-   Use `set` whenever ordering matters.
-   Prefer `unordered_set` when ordering is not required and average
    O(1) lookup is sufficient.
-   `lower_bound()` and `upper_bound()` are powerful tools for interval
    and binary-search style problems.
-   Never expect indexing support from a set.
