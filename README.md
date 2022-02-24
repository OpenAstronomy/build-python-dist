## build-python-dist

[![.github/workflows/main.yml](https://github.com/OpenAstronomy/build-python-dist/actions/workflows/test_action.yml/badge.svg)](https://github.com/OpenAstronomy/build-python-dist/actions/workflows/test_action.yml)

An experimental GitHub action to build and test source distributions for
Python packages, and optionally a wheel for pure Python packages.

## Examples

### Build a source distribution with no testing:

```yaml
jobs:
  build_sdist:
    name: Build source distribution
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - id: build
        uses: OpenAstronomy/build-python-dist@main
```

### Build a source distribution with testing

```yaml
jobs:
  build_sdist:
    name: Build source distribution
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - id: build
        uses: OpenAstronomy/build-python-dist@main
        with:
          test_extras: test
          test_command: pytest --pyargs test_package
```

The ``test_extras`` option, if specified, should contain a string (e.g. ``test`` or ``test,all``) that will be used to determine which 'extras' should be installed when testing. The ``test_command`` option should contain the full command to use for testing the installed package (this is run from an empty temporary directory).

### Build a source distribution and wheel for a pure-Python package

```yaml
jobs:
  build_sdist_and_wheel:
    name: Build source distribution and pure-Python wheel
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - id: build
        uses: OpenAstronomy/build-python-dist@main
        with:
          pure_python_wheel: true
          test_extras: test
          test_command: pytest --pyargs test_package
```

## Notes

To build wheels for packages with extensions, you should instead use
[cibuildwheel](https://github.com/pypa/cibuildwheel) which includes
a GitHub action for convenience.
