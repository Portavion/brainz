---
title: "Upacking"
source: "https://www.w3schools.com/python/python_tuples_unpack.asp"
author:
published:
created: 2025-04-11
description: "Python methods for unpacking"
tags:
  - "python"
---
# Python Unpacking
## Unpacking a Tuple
When we create a tuple, we normally assign values to it. This is called "packing" a tuple:

- Packing a tuple:
```python
fruits = ( "apple", "banana", "cherry" )  
```
- unpacking a tuple
```python
fruits = ( "apple", "banana", "cherry" )  
  
(green, yellow, red) = fruits  
  
print (green)  
print (yellow)  
print (red)
```
**Note:** The number of variables must match the number of values in the tuple, if not, you must use an asterisk to collect the remaining values as a list.
## Using Asterisk\*
If the number of variables is less than the number of values, you can add an `*` to the variable name and the values will be assigned to the variable as a list:

Assign the rest of the values as a list called "red":
```python
fruits = ( "apple", "banana", "cherry", "strawberry", "raspberry" )  
  
(green, yellow, \*red) = fruits  
  
print (green)  
print (yellow)  
print (red)
```
If the asterisk is added to another variable name than the last, Python will assign values to the variable until the number of values left matches the number of variables left.

Add a list of values the "tropic" variable:
```python
fruits = ( "apple", "mango", "papaya", "pineapple", "cherry" )  
  
(green, \*tropic, red) = fruits  
  
print (green)  
print (tropic)  
print (red)

```