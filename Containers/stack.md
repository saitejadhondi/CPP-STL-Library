# C++ STL - Stack (`std::stack`)

> Interview-focused notes on the C++ STL Stack.

------------------------------------------------------------------------

# What is a Stack?

A **stack** is a linear data structure that follows the **LIFO (Last In,
First Out)** principle.

The last element inserted is the first one removed.

Example:

    Push: 10
    Push: 20
    Push: 30

    Top -> 30

    Pop()

    Top -> 20

Think of a stack of plates: you always add and remove from the top.

------------------------------------------------------------------------

# Where is Stack Used?

-   Function call stack
-   Undo/Redo operations
-   Browser history
-   Parentheses matching
-   Expression evaluation
-   DFS (Depth First Search)
-   Backtracking

------------------------------------------------------------------------

# Declaration

``` cpp
#include <stack>

stack<int> st;
stack<string> st2;
stack<pair<int,int>> st3;
```

------------------------------------------------------------------------

# Important Functions

## push()

Adds an element to the top.

``` cpp
st.push(10);
st.push(20);
st.push(30);
```

Stack:

    30 <- Top
    20
    10

Time Complexity: **O(1)**

------------------------------------------------------------------------

## pop()

Removes the top element.

``` cpp
st.pop();
```

After pop:

    20 <- Top
    10

> `pop()` does **not** return the removed value.

Time Complexity: **O(1)**

------------------------------------------------------------------------

## top()

Returns the top element.

``` cpp
cout << st.top();
```

Output:

    30

Time Complexity: **O(1)**

------------------------------------------------------------------------

## size()

Returns the number of elements.

``` cpp
st.size();
```

Time Complexity: **O(1)**

------------------------------------------------------------------------

## empty()

Checks whether the stack is empty.

``` cpp
if(st.empty())
```

Returns `true` or `false`.

Time Complexity: **O(1)**

------------------------------------------------------------------------

# Traversing a Stack

A stack does **not** support indexing or iterators.

The only way to traverse it is by repeatedly accessing the top and
popping elements.

``` cpp
while(!st.empty())
{
    cout << st.top() << " ";
    st.pop();
}
```

> Traversing like this **destroys the stack**.

If you want to preserve it:

``` cpp
stack<int> temp = st;

while(!temp.empty())
{
    cout << temp.top() << " ";
    temp.pop();
}
```

------------------------------------------------------------------------

# Complete Example

``` cpp
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<int> st;

    st.push(10);
    st.push(20);
    st.push(30);

    cout << st.top() << endl;

    st.pop();

    cout << st.top() << endl;

    cout << st.size() << endl;

    cout << st.empty() << endl;

    return 0;
}
```

Output:

    30
    20
    2
    0

------------------------------------------------------------------------

# Time Complexity

  Operation   Complexity
  ----------- ------------
  push()      O(1)
  pop()       O(1)
  top()       O(1)
  size()      O(1)
  empty()     O(1)

------------------------------------------------------------------------

# Interview Questions

## Why can't we access the middle element?

A stack intentionally exposes only the **top** element to enforce the
LIFO principle.

------------------------------------------------------------------------

## Difference between Stack and Queue

  Stack                  Queue
  ---------------------- -----------------------------------
  LIFO                   FIFO
  Insert/Delete at Top   Insert at Back, Delete from Front
  `top()`                `front()` / `back()`

------------------------------------------------------------------------

## Can we iterate using a `for` loop?

No. `std::stack` provides no iterators or indexing.

------------------------------------------------------------------------

## What is the underlying container?

By default:

``` cpp
deque<T>
```

You can also use:

``` cpp
stack<int, vector<int>> st;
stack<int, list<int>> st;
```

------------------------------------------------------------------------

# Common Coding Problems

1.  Valid Parentheses
2.  Next Greater Element
3.  Previous Greater Element
4.  Largest Rectangle in Histogram
5.  Min Stack
6.  Evaluate Postfix Expression
7.  Infix to Postfix
8.  Infix to Prefix
9.  Reverse a Stack
10. Sort a Stack using Recursion

------------------------------------------------------------------------

# Tips

-   Always check `empty()` before calling `top()` or `pop()`.
-   `pop()` returns nothing.
-   Use a temporary copy if you need to print without modifying the
    original stack.
