# What is UV?

UV is a python package manager, that is used to manage packages in a python project. It can also be used to manage
python installation. It is one of the fastest package manager and build ground-up using Rust.

UV supports installation of additional tools like Ruff or black, without installing it in the main project.

## High level commands

1. Managing Python itself (Currently in public preview)
    * uv python install : install a specific version of python
    * uv python find : find an installed version of python
2. Executing a standalone pythong script
    * uv run : Run a python script
    * uv add --script : Add a dependency to a script
3. Managing python projects
    * uv init : create a new python project
    * uv add : Add a dependency to the project
    * uv remove: Remove a dependency from a project
    * uv sync : Sync the project's dependency with the environment
    * uv lock : Create a lock file for project's dependency
    * uv run : Run a command in a project's environment
    * uv tree : View the dependency tree of the project.
    * uv build : Build the project into distribution archives
        * It tells UV to package the python project into standard python distribution.
            * Wheel (.whl) : A built package, ready to install.
            * Source Distribution (.tar.gz) : The raw source code packaged up, which can be used to build the wheel or
              install directly.
        * This is part of the python packaging workflow (similar to python -m build or setuptools)
        * This command would mostly be used publishing the python project(eg, PyPI) or for sharing or distributing in
          general.
4. Tools
    * uvx / uv tool run : Run a tool in a temporary environment
    * uv tool install : Install a tool user-wide
    * uv tool uninstall : Uninstall a tool
    * uv tool list : List installed tools
    * uv tool update-shell : Update the shell to include tool executable. 

5. pip interface : Usually used with older versions of projects.
   * uv pip install : Install packages into the current environment.
   * uv pip show : Show details about an installed package
   * uv pip list : List installed packages

6. UV level utility
   * uv cache clean: Remove cache entries.
   * uv cache prune: Remove outdated cache entries.
   * uv cache dir: Show the uv cache dir.
   * uv tool dir: show the uv tool dir.
   * uv python dir: show the uv installed Python version paths.
   * uv self update: Update uv to the latest version



---
* Reference
  * https://github.com/astral-sh/uv/issues/9219
  * 