# Tests
Currently most of the code is not tested. The project has a basic `tox` setup
which performs simple tests using `pytest` and generates documentation using 
`sphinx`. The tests are far from complete.

Use `tox` command to run the tests:
```
tox
```

## Configuration files explained
- `setup.cfg` is a configuration for setuptools.
- `tox.ini` defines what does the `tox` command do.
- sphinx configuration is inside `sphinx_config/conf.py` file.
- `sphinx_config/index.rst` defines the content of `index.html` file generated
  with sphinx. There are other `rst` files that define other pages.
- sphinx documentation is generated into `documentation/` path which is
  excluded with `.gitignore`
- All test functions should have name compliant to these patterns: `test_*` or
  `*_test` (it's required by `pytest`).

# Publishing documentation
This code uses Github pages for documentation. The github pages code is
a copy of `documentation/` directory moved to `gh-pages` branch.

You can use the `mv_documentation.py` script to copy content of the
`documentation/` folder (generated with `tox`) to `gh-pages` branch in order
to publish it.

The script checkouts to the `gh-pages` branch, removes all fiels
and moves the content of `documentation/` directory to root directory. If you
want to stage and commit that changes you have to do that manually.

# Submodules
The project uses a git submodule for the source code. I intend to use the same
source on other projects where installing and importing Python packages
normally is not possible (blender addons) therefore I need to copy the source
code to the project.

Changes to submodules can be commited with using `git submodule foreach`
command with the same comment as the main project. Example:
```
git submodule foreach "git add -A"
git submodule foreach "git commit -m 'Some comment.'"
```

# Project configuration
As of the writing of this document `setuptools` uses `setup.cfg` and the
`pyproject.toml` is in beta. I expect that in the future everything will be
moved to `pyproject.toml` file. Currently the `pyproject.toml` file only
specifies that the project uses `setuptools` which is a default setting making
this file redundant.
