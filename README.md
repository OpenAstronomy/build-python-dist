An experimental GitHub action to build and test source distributions for
Python packages, and optionally a wheel for pure Python packages.

Example usage to build a source distribution:

```
jobs:

  build_sdist:
    name: Build source distribution
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - id: build
        uses: OpenAstronomy/action-build-sdist-and-wheel@main
        with:
          test_extras: test
          test_command: pytest --pyargs test_package
```

The ``test_extras`` and ``test_command`` are optional but recommended.

For pure-Python packages, you can also build a pure-Python wheel by modifying
the above example::

```
jobs:
  build_sdist_and_wheel:
    name: Build source distribution and pure-Python wheel
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - id: build
        uses: OpenAstronomy/action-build-sdist-and-wheel@main
        with:
          pure_python_wheel: true
          test_extras: test
          test_command: pytest --pyargs test_package
```

To build wheels for packages with extensions, you should instead use
[cibuildwheel](https://github.com/pypa/cibuildwheel) which includes
a GitHub action for convenience.
