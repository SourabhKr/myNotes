# Function Arguments

1. Pass by reference
2. Pass by Value:

Pass by reference is something when we pass the reference of a variable to the function. 
> From Realpython: By reference means that the argument you’re passing to the function is a reference to a variable that already exists in memory rather than an independent copy of that variable

Pass by value is when we pass a copy of the variable to the function. 
In pythons it’s neither pass by value not pass by reference, though it’s pass by assignment. 

Python passes arguments by assignment. That is, when you call a Python function, each function argument becomes a variable to which the passed value is assigned.

1. Function arguments initially refer to the same address as their original variables.
2. Reassigning the argument within the function gives it a new address while the original variable remains unmodified.

![Example](/images/python/arguments.jpg)

Assignment in Python:

* If the assignment target is an identifier, or variable name, then this name is bound to the object. For example, in x = 2, x is the name and 2 is the object.
* If the name is already bound to a separate object, then it’s re-bound to the new object. For example, if x is already 2 and you issue x = 3, then the variable name x is re-bound to 3.

---
Reference:

1. RealPython
