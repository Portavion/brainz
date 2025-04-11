---
title: "Deque"
source: "https://docs.python.org/3/library/collections.html#collections.deque"
author:
  - "[[Python documentation]]"
published:
created: 2025-04-11
description: "Source code: Lib/collections/__init__.py This module implements specialized container datatypes providing alternatives to Python’s general purpose built-in containers, dict, list, set, and tuple.,,..."
tags:
  - "python datastructure"
---
# [`deque`](https://docs.python.org/3/library/collections.html#collections.deque "collections.deque") objects[](https://docs.python.org/3/library/collections.html#deque-objects "Link to this heading")
_class_ collections.deque([_iterable_[, _maxlen_]])[](https://docs.python.org/3/library/collections.html#collections.deque "Link to this definition")

Returns a new deque object initialized left-to-right (using [`append()`](https://docs.python.org/3/library/collections.html#collections.deque.append "collections.deque.append")) with data from _iterable_. If _iterable_ is not specified, the new deque is empty.

Deques are a generalization of stacks and queues (the name is pronounced “deck” and is short for “double-ended queue”). Deques support thread-safe, memory efficient appends and pops from either side of the deque with approximately the same _O_(1) performance in either direction.

Though [`list`](https://docs.python.org/3/library/stdtypes.html#list "list") objects support similar operations, they are optimized for fast fixed-length operations and incur _O_(_n_) memory movement costs for `pop(0)` and `insert(0, v)` operations which change both the size and position of the underlying data representation.

If _maxlen_ is not specified or is `None`, deques may grow to an arbitrary length. Otherwise, the deque is bounded to the specified maximum length. Once a bounded length deque is full, when new items are added, a corresponding number of items are discarded from the opposite end. Bounded length deques provide functionality similar to the `tail` filter in Unix. They are also useful for tracking transactions and other pools of data where only the most recent activity is of interest.
## Methods

- append(_x_)[](https://docs.python.org/3/library/collections.html#collections.deque.append "Link to this definition"): Add _x_ to the right side of the deque.
- appendleft(_x_)[](https://docs.python.org/3/library/collections.html#collections.deque.appendleft "Link to this definition"): Add _x_ to the left side of the deque.
- clear()[](https://docs.python.org/3/library/collections.html#collections.deque.clear "Link to this definition"): Remove all elements from the deque leaving it with length 0.
- copy()[](https://docs.python.org/3/library/collections.html#collections.deque.copy "Link to this definition"): Create a shallow copy of the deque. Added in version 3.5.
- count(_x_)[](https://docs.python.org/3/library/collections.html#collections.deque.count "Link to this definition") Count the number of deque elements equal to _x_. Added in version 3.2.
- extend(_iterable_)[](https://docs.python.org/3/library/collections.html#collections.deque.extend "Link to this definition") Extend the right side of the deque by appending elements from the iterable argument.
- extendleft(_iterable_)[](https://docs.python.org/3/library/collections.html#collections.deque.extendleft "Link to this definition") Extend the left side of the deque by appending elements from _iterable_. Note, the series of left appends results in reversing the order of elements in the iterable argument.
- index(_x_[, _start_[, _stop_]])[](https://docs.python.org/3/library/collections.html#collections.deque.index "Link to this definition") Return the position of _x_ in the deque (at or after index _start_ and before index _stop_). Returns the first match or raises [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError "ValueError") if not found. Added in version 3.5.
- insert(_i_, _x_)[](https://docs.python.org/3/library/collections.html#collections.deque.insert "Link to this definition") Insert _x_ into the deque at position _i_. If the insertion would cause a bounded deque to grow beyond _maxlen_, an [`IndexError`](https://docs.python.org/3/library/exceptions.html#IndexError "IndexError") is raised. Added in version 3.5.
- pop()[](https://docs.python.org/3/library/collections.html#collections.deque.pop "Link to this definition") Remove and return an element from the right side of the deque. If no elements are present, raises an [`IndexError`](https://docs.python.org/3/library/exceptions.html#IndexError "IndexError").
- popleft()[](https://docs.python.org/3/library/collections.html#collections.deque.popleft "Link to this definition") Remove and return an element from the left side of the deque. If no elements are present, raises an [`IndexError`](https://docs.python.org/3/library/exceptions.html#IndexError "IndexError").
- remove(_value_)[](https://docs.python.org/3/library/collections.html#collections.deque.remove "Link to this definition") Remove the first occurrence of _value_. If not found, raises a [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError "ValueError").
- reverse()[](https://docs.python.org/3/library/collections.html#collections.deque.reverse "Link to this definition") Reverse the elements of the deque in-place and then return `None`. Added in version 3.2.
- rotate(_n=1_)[](https://docs.python.org/3/library/collections.html#collections.deque.rotate "Link to this definition") Rotate the deque _n_ steps to the right. If _n_ is negative, rotate to the left. When the deque is not empty, rotating one step to the right is equivalent to `d.appendleft(d.pop())`, and rotating one step to the left is equivalent to `d.append(d.popleft())`.

Deque objects also provide one read-only attribute:
- maxlen[](https://docs.python.org/3/library/collections.html#collections.deque.maxlen "Link to this definition") Maximum size of a deque or `None` if unbounded. Added in version 3.1.

In addition to the above, deques support iteration, pickling, `len(d)`, `reversed(d)`, `copy.copy(d)`, `copy.deepcopy(d)`, membership testing with the [`in`](https://docs.python.org/3/reference/expressions.html#in) operator, and subscript references such as `d[0]` to access the first element. Indexed access is _O_(1) at both ends but slows to _O_(_n_) in the middle. For fast random access, use lists instead.

Starting in version 3.5, deques support `__add__()`, `__mul__()`, and `__imul__()`.
## Example:
```python
from collections import deque

d = deque('ghi')                 # make a new deque with three items

for elem in d:                   # iterate over the deque's elements

    print(elem.upper())
G
H
I

d.append('j')                    # add a new entry to the right side

d.appendleft('f')                # add a new entry to the left side

d                                # show the representation of the deque
deque(['f', 'g', 'h', 'i', 'j'])

d.pop()                          # return and remove the rightmost item
'j'

d.popleft()                      # return and remove the leftmost item
'f'

list(d)                          # list the contents of the deque
['g', 'h', 'i']

d[0]                             # peek at leftmost item
'g'

d[-1]                            # peek at rightmost item
'i'

list(reversed(d))                # list the contents of a deque in reverse
['i', 'h', 'g']

'h' in d                         # search the deque
True

d.extend('jkl')                  # add multiple elements at once

d
deque(['g', 'h', 'i', 'j', 'k', 'l'])

d.rotate(1)                      # right rotation

d
deque(['l', 'g', 'h', 'i', 'j', 'k'])

d.rotate(-1)                     # left rotation

d
deque(['g', 'h', 'i', 'j', 'k', 'l'])

deque(reversed(d))               # make a new deque in reverse order
deque(['l', 'k', 'j', 'i', 'h', 'g'])

d.clear()                        # empty the deque

d.pop()                          # cannot pop from an empty deque
Traceback (most recent call last):
    File "<pyshell#6>", line 1, in -toplevel-
        d.pop()
IndexError: pop from an empty deque

d.extendleft('abc')              # extendleft() reverses the input order

d
deque(['c', 'b', 'a'])

```
# [`deque`](https://docs.python.org/3/library/collections.html#collections.deque "collections.deque") Recipes[](https://docs.python.org/3/library/collections.html#deque-recipes "Link to this heading")

This section shows various approaches to working with deques.

Bounded length deques provide functionality similar to the `tail` filter in Unix:

def tail(filename, n=10):
    'Return the last n lines of a file'
    with open(filename) as f:
        return deque(f, n)

Another approach to using deques is to maintain a sequence of recently added elements by appending to the right and popping to the left:

def moving_average(iterable, n=3):
# moving_average([40, 30, 50, 46, 39, 44]) --> 40.0 42.0 45.0 43.0
# <https://en.wikipedia.org/wiki/Moving_average>
    it = iter(iterable)
    d = deque(itertools.islice(it, n-1))
    d.appendleft(0)
    s = sum(d)
    for elem in it:
        s += elem - d.popleft()
        d.append(elem)
        yield s / n

A [round-robin scheduler](https://en.wikipedia.org/wiki/Round-robin_scheduling) can be implemented with input iterators stored in a [`deque`](https://docs.python.org/3/library/collections.html#collections.deque "collections.deque"). Values are yielded from the active iterator in position zero. If that iterator is exhausted, it can be removed with [`popleft()`](https://docs.python.org/3/library/collections.html#collections.deque.popleft "collections.deque.popleft"); otherwise, it can be cycled back to the end with the [`rotate()`](https://docs.python.org/3/library/collections.html#collections.deque.rotate "collections.deque.rotate") method:

def roundrobin(*iterables):
    "roundrobin('ABC', 'D', 'EF') --> A D E B F C"
    iterators = deque(map(iter, iterables))
    while iterators:
        try:
            while True:
                yield next(iterators[0])
                iterators.rotate(-1)
        except StopIteration:
# Remove an Exhausted Iterator.
            iterators.popleft()

The [`rotate()`](https://docs.python.org/3/library/collections.html#collections.deque.rotate "collections.deque.rotate") method provides a way to implement [`deque`](https://docs.python.org/3/library/collections.html#collections.deque "collections.deque") slicing and deletion. For example, a pure Python implementation of `del d[n]` relies on the `rotate()` method to position elements to be popped:

def delete_nth(d, n):
    d.rotate(-n)
    d.popleft()
    d.rotate(n)

To implement [`deque`](https://docs.python.org/3/library/collections.html#collections.deque "collections.deque") slicing, use a similar approach applying [`rotate()`](https://docs.python.org/3/library/collections.html#collections.deque.rotate "collections.deque.rotate") to bring a target element to the left side of the deque. Remove old entries with [`popleft()`](https://docs.python.org/3/library/collections.html#collections.deque.popleft "collections.deque.popleft"), add new entries with [`extend()`](https://docs.python.org/3/library/collections.html#collections.deque.extend "collections.deque.extend"), and then reverse the rotation. With minor variations on that approach, it is easy to implement Forth style stack manipulations such as `dup`, `drop`, `swap`, `over`, `pick`, `rot`, and `roll`.