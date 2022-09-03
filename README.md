> This README file is for mostly a note to myself about the structure of the
> project. I need this because I know I won't spend a lot of time on its
> maintenance and long breaks are expected. If you're looking for documentation
> please visit: https://nusiq.github.io/better_json/


# Better JSON
My set of tools for working with JSON that I used to constantly copy between
my projects.

## Features
- **Compact encoder** - better JSON formatting.
- **JSONC Decoder** - reading JSONC files.
- **JSON Walkers** - better navigation through JSON objects.

# Info about the project
## Tests
Currently most of the code is not tested. There is some basic `tox` setup
for testing the project and generaring documentation but the code lacks tests.

To test execute command below in root directory:
```
tox
```

Additionally you can run `doctest` tests for `src/better_json/__init__.py`
file by executing command below in `src/better_json` directory:
```
python -m doctest .\__init__.py
```

###= Configuration files explained
- `setup.cfg` is a configuration for `setup.py`.
- `tox.ini` is `tox` configuration which creates one test environemnt and
defines what does the `tox` command do (it runs unittests using `pytest` and
creates documentation using `sphinx`)
- sphinx configuration is inside `sphinx_config/conf.py` file.
- `sphinx_config/index.rst` defines the content of `index.html` file generated
with sphinx. There are other `rst` files that define other pages.
- sphinx documentation is created inside `documentation/` path which is
excluded with `.gitignore`
- All test functions should have name compliant to this patterns: `test_*` or
`*_test`. It's required by `pytest`

## Publishing documentation
This code uses Github pages for documentation. The github pages code is
a copy of `documentation/` directory moved to `gh-pages` branch.

You can use the `mv_documentation.py` script to copy content of the
`documentation/` folder (generated with `tox`) to `gh-pages` branch in order
to publish it.

The script checkouts to the `gh-pages` branch, removes all fiels
and moves the content of `documentation/` directory to root directory. If you
want to stage and commit that changes you have to do that manually.

## Submodules
The project uses a git submodule for the source code. I intend to use the same
sourec on other projects where installing and importing Python packages
normally is not possible (blender addons) therefore I need to copy the source
code to the project.

Changes to submodules can be commited with using `git submodule foreach`
command with the same comment as the main project. Example:
```
git submodule foreach "git add -A"
git submodule foreach "git commit -m 'Some comment.'"
```
