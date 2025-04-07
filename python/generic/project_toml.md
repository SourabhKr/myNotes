# project.toml file

project.toml file is the configuration file used by the packaging tools, as well as other tools such as linters, type
checkers etc. There are three possible tables in this file.

`[build-system]` table: It allows choosing a build backend with the dependencies needed to build the project.

`[project]` table : Used to define the metadata of a project, such as project name, dependencies, version etc...

The `[tool]` table : has tool-specific `subtables`, e.g., `[tool.hatch]`, `[tool.black]`, `[tool.mypy]`.

## [build-system]

build-system contains a build-backend key, that specifies the backend to be used. It also contains a requirements key,
which is a list of dependencies needed to build the project – this is typically just the build backend package, but it
may also contain additional dependencies.

```toml
[build-system]
requires = ["setuptools >= 77.0.3"]
build-backend = "setuptools.build_meta"
```

## [project]

### static vs dynamic metadata

In most of the cases the metadata defined in the project is static, ex `required-python=">=3.8"` or `version = "1.0"`.
However, in some cases it is helpful to let the build backend compute the metadata. For example: many build backends can
read the version from a `__version__` attribute from the code, a Git tag, or similar. In such cases, making the field
dynamic is advisable. When a field is dynamic, it is the build backend’s responsibility to fill it.

```toml
[project]
dynamic = ["version"]
```

### name

Put the name of the project on PyPI. This field is a required field and the only one that can't be marked as `dynamic`.




Properties
----
Reference

* https://packaging.python.org/en/latest/guides/writing-pyproject-toml/
* https://packaging.python.org/en/latest/glossary/#term-Build-Backend
