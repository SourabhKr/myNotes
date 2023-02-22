# Variables in Python

---
Variables in python is bit different then what we see in c, c++, java etc. In python the variables are always a reference variable, i.e. refer to a memory location where the object is stored.

To discuss it in details let's understand how the program is executed. When a python file is executed the interpreter first allocates two set of memories, Heap and Stack. The size of memory is governed by python version, os and environment settings etc..

The first set is called the Heap memory and another one is called the Stack memory as show in the figure below.
Once we initiate a variable with a value, the interpreter in background allocates Heap memory based on the type of value getting created for example, for int, in python it will allocate 4 bytes. The value created will be referenced by the variable(identifier to be precised).

```python
main.py

x = 10
z = fn()

def fn():
  y = 10
  return y + 1
```

![Memory Allocation](/images/python/PythonVariable.jpg)

 In python everything is an object and this is true in a sense as even primitive data types are also objects.

---

## **Link**

* <https://www.youtube.com/watch?v=arxWaw-E8QQ&list=PLTdyJRA-IxGa9eU_VOeZRfSMPk7b4ZaEl>
* <https://www.pythontutorial.net/advanced-python/python-references/>
