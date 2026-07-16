# C++ STL - Vector (`std::vector`)

> Interview-focused notes based on the STL repository shared by the
> user, with additional explanations.

------------------------------------------------------------------------

## Learning path

- Previous: Start here
- Next: [Stack](stack.md)
- Related: [Queue](queue.md), [Deque](deque.md)

------------------------------------------------------------------------

# What is a Vector?

A **vector** is a **dynamic array** provided by the C++ Standard
Template Library (STL).

Unlike a normal array whose size is fixed, a vector automatically grows
and shrinks as elements are inserted or removed.

``` cpp
vector<int> v;
```

Initially:

``` text
[]
```

``` cpp
v.push_back(10);
v.push_back(20);
v.push_back(30);
```

Output:

``` text
[10, 20, 30]
```

------------------------------------------------------------------------

# Why use a Vector?

A normal array:

``` cpp
int arr[5];
```

cannot store more than 5 elements.

A vector automatically allocates more memory whenever needed.

------------------------------------------------------------------------

# Internal Memory Growth

Suppose capacity is 4:

``` text
10 20 30 _
```

Insert another element:

``` text
10 20 30 40
```

Insert one more:

``` text
10 20 30 40 50
```

The vector allocates a larger memory block (typically doubling the
capacity), copies the existing elements, deletes the old block, and
continues.

This is why `push_back()` has **amortized O(1)** complexity.

------------------------------------------------------------------------

# Size vs Capacity

  Property   Meaning
  ---------- -------------------------------------
  Size       Number of elements currently stored
  Capacity   Memory currently allocated

Example:

``` cpp
vector<int> v;
```

  Operation         Size   Capacity
  --------------- ------ ----------
  Initially            0          0
  push_back(10)        1          1
  push_back(20)        2          2
  push_back(30)        3          4
  push_back(40)        4          4
  push_back(50)        5          8

------------------------------------------------------------------------

# Declaration

``` cpp
vector<int> v;
vector<int> v(5);
vector<int> v(5,100);
vector<int> v = {1,2,3,4};

vector<vector<int>> mat;
vector<vector<int>> mat(3, vector<int>(4,0));
```

------------------------------------------------------------------------

# Important Functions

## push_back()

Adds an element at the end.

``` cpp
v.push_back(10);
```

Time Complexity: **Amortized O(1)**

------------------------------------------------------------------------

## emplace_back()

Constructs the object directly inside the vector.

``` cpp
vector<pair<int,int>> v;

v.push_back({1,2});
v.emplace_back(1,2);
```

For primitive types there is almost no difference.

For complex objects, `emplace_back()` avoids creating an unnecessary
temporary object.

------------------------------------------------------------------------

## pop_back()

Removes the last element.

``` cpp
v.pop_back();
```

Time Complexity: **O(1)**

------------------------------------------------------------------------

## size()

``` cpp
v.size();
```

Returns the number of elements.

------------------------------------------------------------------------

## empty()

``` cpp
v.empty();
```

Returns `true` if empty.

------------------------------------------------------------------------

## clear()

``` cpp
v.clear();
```

Removes all elements.

> Note: Capacity usually remains allocated.

------------------------------------------------------------------------

## front()

Returns the first element.

``` cpp
v.front();
```

------------------------------------------------------------------------

## back()

Returns the last element.

``` cpp
v.back();
```

------------------------------------------------------------------------

## at()

``` cpp
v.at(2);
```

Performs bounds checking.

`v[2]` does not.

------------------------------------------------------------------------

## insert()

``` cpp
v.insert(v.begin()+2,100);
```

Time Complexity: **O(n)**

------------------------------------------------------------------------

## erase()

``` cpp
v.erase(v.begin()+1);
```

Time Complexity: **O(n)**

------------------------------------------------------------------------

# Traversing a Vector

## Index

``` cpp
for(int i=0;i<v.size();i++)
    cout<<v[i];
```

## Range-based loop

``` cpp
for(auto x:v)
    cout<<x;
```

## Iterator

``` cpp
for(auto it=v.begin();it!=v.end();it++)
    cout<<*it;
```

------------------------------------------------------------------------

# Common STL Algorithms

``` cpp
sort(v.begin(),v.end());
sort(v.begin(),v.end(),greater<int>());
reverse(v.begin(),v.end());
find(v.begin(),v.end(),5);
count(v.begin(),v.end(),10);

*max_element(v.begin(),v.end());
*min_element(v.begin(),v.end());
```

------------------------------------------------------------------------

# Time Complexity

  Operation    Complexity
  ------------ ----------------
  Access       O(1)
  push_back    Amortized O(1)
  pop_back     O(1)
  front/back   O(1)
  size         O(1)
  empty        O(1)
  insert       O(n)
  erase        O(n)
  sort         O(n log n)

------------------------------------------------------------------------

# Interview Questions

## Difference between Array and Vector

  Array                Vector
  -------------------- --------------------
  Fixed size           Dynamic size
  Limited operations   Rich STL support
  Manual resizing      Automatic resizing

------------------------------------------------------------------------

## Difference between push_back() and emplace_back()

-   `push_back()` inserts an existing object.
-   `emplace_back()` constructs the object directly in place.

------------------------------------------------------------------------

## Why is push_back() amortized O(1)?

Because reallocation happens only occasionally when the current capacity
becomes full.

------------------------------------------------------------------------

## When should insert() be avoided?

Avoid inserting in the middle frequently because every insertion shifts
elements, making it **O(n)**.

------------------------------------------------------------------------

# Practice Questions

1.  Reverse a vector.
2.  Remove all occurrences of a value.
3.  Find the second largest element.
4.  Rotate a vector by K positions.
5.  Merge two sorted vectors.
6.  Remove duplicates from a sorted vector.
7.  Find the frequency of every element.
8.  Sort in descending order.
9.  Find minimum and maximum elements.
10. Insert an element at a given index.

------------------------------------------------------------------------

**Source:** Based on the STL notes shared in the conversation, expanded
with interview-focused explanations.
