
# Better JSON
My set of tools for working with JSON that I used to constantly copy between
my projects.

# Modules
## Compact encoder
A simple python module that adds CompactEncoder class for better json
formatting.

# JSONC Decoder
TODO

# JSON Walker
TODO



# Info about the project
This module provides some tools to deal with JSON and JSONC more efficiently
but its main purpose for me was to learn how to setup a python project with
unittests supported by `tox` and with automatically generated documentation
using `sphinx`.

## Tests
Execute command below in root directory:
```
tox
```
Additionally you can run `doctest` tests for `src/better_json/__init__.py`
file by executing command below in `src/better_json` directory:
```
python -m doctest .\__init__.py
```

### Configuration files explained
- `setup.cfg` is a configuration for `setup.py`.
- `tox.ini` is `tox` configuration which creates one test environemnt and
defines what does the `tox` command do (it runs unittests using `pytest` and
creates documentation using `sphinx`)
- sphinx configuration is inside `sphinx_config/conf.py` file.
- `sphinx_config/index.rst` defines the content of `index.html` file generated
with sphinx.
- sphinx documentation is created inside `documentation/` path which is
excluded with `.gitignore`
- All test functions should have name compliant to this patterns: `test_*` or
`*_test`. It's required by `pytest`

## Documentation
This code uses Github pages for documentation. The github pages code is
a copy of `documentation/` directory moved to `gh-pages` branch. You
can visit the documentation page at https://nusiq.github.io/better_json/ 
Github pages link is automatically generated with this pattern:
```
<USERNAME>.github.io/<REPOSITORY NAME>/
```

### Coping documentation to gh-pages
You can use the `mv_documentation.py` script to copy content of the
`documentation/` folder (generated with `tox`) to `gh-pages` branch in order
to publish it.

The script checkouts to the `gh-pages` branch, removes all fiels
and moves the content of `documentation/` directory to root directory. If you
want to stage and commit that changes you have to do that manually.
