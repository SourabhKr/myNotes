# Why do we need virtual environment?

As the name suggests virtual environments are used to create lightweight, disposable isolated environments. When we create a virtual environment, a new folder structure which contains the python binary and the package dependencies is created(the python binary is either copied or a sim-link is created to the existing python binary).

Virtual environments and pyenv are a match made in heaven. pyenv has a wonderful plugin called pyenv-virtualenv that makes working with multiple Python version and multiple virtual environments a breeze. If you’re wondering what the difference is between pyenv, pyenv-virtualenv, and tools like virtualenv or venv, then don’t worry. You’re not alone.

Here’s what you need to know:

* pyenv manages multiple versions of Python itself.
* virtualenv/venv manages virtual environments for a specific Python version.
    1. Virtualenv is a superset of venv and provides the basis for its implementation. It’s a powerful, extendable tool for creating isolated Python environments.
    2. Conda offers package, dependency, and environment management for Python and other languages.
* poetry: Another virtual environment manager, similar to the inbuilt venv, with added features on top to manage the package dependency and overall building and packaging.
* pyenv-virtualenv manages virtual environments for across varying versions of python.

---
Reference:

1. <https://realpython.com/python-virtual-environments-a-primer/>
2. <https://realpython.com/intro-to-pyenv/>
