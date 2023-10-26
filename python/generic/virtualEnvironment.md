# Why do we need different Python Versions?

Usually Python is pre-installed in all the OS providers and mostly installed at */usr/bin/python*. Hence, updating the
Python version or installing new packages will install it globally. This can have problems as we can update OS related
packages/python version which are required by the OS to function properly, and updating the same can break the OS.

## What is the difference between pyenv and virtual environments?

pyenv is used to maintain multiple versions of pythons whereas virtual environments are used to maintain different
packages which isolates project level dependency. To give an example, if the requirement to build multiple applications
that need different python versions, one application needing a version 3.9 and another 3.12. To facilitate this we need
pyenv. On the other hand different libraries in python 3.9 can have dependency issues between different libraries this
can be solved by using virtual environments.

As the name suggests virtual environments are used to create lightweight, disposable isolated environments. When we
create a virtual environment, a new folder structure which contains the python binary and the package dependencies is
created(the python binary is either copied or a sim-link is created to the existing python binary).

Virtual environments and pyenv are a match made in heaven. pyenv has a wonderful plugin called pyenv-virtualenv that
makes working with multiple Python version and multiple virtual environments a breeze. If you’re wondering what the
difference is between pyenv, pyenv-virtualenv, and tools like virtualenv or venv, then don’t worry. You’re not alone.

Here’s what you need to know:

* pyenv manages multiple versions of Python itself.
* virtualenv/venv manages virtual environments for a specific Python version.
    1. Virtualenv is a superset of venv and provides the basis for its implementation. It’s a powerful, extendable tool
       for creating isolated Python environments.
    2. Conda offers package, dependency, and environment management for Python and other languages.
* poetry: Another virtual environment manager, similar to the inbuilt venv, with added features on top to manage the
  package dependency and overall building and packaging.
* pyenv-virtualenv manages virtual environments for across varying versions of python.

---
Reference:

1. <https://realpython.com/python-virtual-environments-a-primer/>
2. <https://realpython.com/intro-to-pyenv/>
