# args and kwargs

*args allows us to pass varying number of positional arguments.
Note that args is just a name. You’re not required to use the name args. You can choose any name that you prefer.

The function still works, even if you pass the iterable object as integers instead of args. All that matters here is that you use the unpacking operator (*). Bear in mind that the iterable object you’ll get using the unpacking operator* is not a list but a tuple. A tuple is similar to a list in that they both support slicing and iteration. However, tuples are very different in at least one aspect: lists are mutable, while tuples are not.

*kwargs works exactly as *args, though the difference is, it’s used for keyword argument.
Like args, kwargs is just a name that can be changed to whatever you want. Again, what is important here is the use of the unpacking operator (**).

Ordering Arguments in a Function
Now that you have learned what *args and **kwargs are for, you are ready to start writing functions that take a varying number of input arguments. But what if you want to create a function that takes a changeable number of both positional and named arguments?
In this case, you have to bear in mind that order counts. Just as non-default arguments have to precede default arguments, so *args must come before**kwargs.
To recap, the correct order for your parameters is:

1. Standard arguments
2. *args arguments
3. **kwargs arguments

Unpacking Operators:
The single asterisk operator * can be used on any iterable that Python provides, while the double asterisk operator ** can only be used on dictionaries.

Reference:

1. realPython