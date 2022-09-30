# Tests
Currently most of the code is not tested. The project has a basic `tox` setup
which performs simple tests using `pytest`.

Use `tox` command to run the tests:
```
tox
```

## Configuration files explained
- `setup.cfg` is a configuration for setuptools.
- `tox.ini` defines what does the `tox` command do.
- sphinx configuration is inside `docs/conf.py` file.
- sphinx documentation can be build using bat script inside `docs` folder.
  In order to build the documentation for local preview `cd` into `docs` folder
  and run `build.bat html` script. The documentation will be available in
  `docs/_build/html` folder.
- All test functions should have name compliant to these patterns: `test_*` or
  `*_test` (it's required by `pytest`).

# Publishing documentation
The projects is set up to publish documentation on readthedocs.org.
This is very basic setup based on the tutorial:
https://docs.readthedocs.io/en/stable/tutorial/

The documentation is build automatically on every commit to the `master`
branch.

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

Pulling changes for submodules:
```
git submodule update --remote --recursive
```

After pulling, if you want to checkout the latest commit from the submodule
you can use:
```
git submodule foreach "git checkout master"
```
(by default it checks out to specific commit)


# Project configuration
As of the writing of this document `setuptools` uses `setup.cfg` and the
`pyproject.toml` is in beta. I expect that in the future everything will be
moved to `pyproject.toml` file. Currently the `pyproject.toml` file only
specifies that the project uses `setuptools` which is a default setting making
this file redundant.

# Building and publishing to PyPI
Resources about packaging: https://packaging.python.org/en/latest/tutorials/packaging-projects/

Update `build` (just in case)
```
python -m pip install --upgrade build
```

Build
```
python -m build
```

Update `twine` (just in case)
```
python3 -m pip install --upgrade twine
```

Upload either to test PyPI or to PyPI
```
# Test PyPI
python3 -m twine upload --repository testpypi dist/*
# PyPI
python3 -m twine upload --repository pypi dist/*
```
The `testpypi` and `pypi` are defined in `~/.pypirc` file with API tokens from
PyPi/TestPyPI.

# Notes about *unusual* commit history of the project
The project started with name `json-encoders` and it only had a single
JSON encoder implementation (the CompactEncoder used in current version).
At that point the module version was slightly above version 1.0.0.

It wasn't imporant for me and I wanted to make a bigger project for JSON
related stuff so I just renamed it to `better-json` and added new
functionallity. After that change the version of the module was set to 2.0.0.
The repository was also renamed to `better-json`.

After polishing the project I decided to publish it on PyPI. The name wasn't
available so the project was renamed once again to `better-json-tools`.
I decided that since the project wasn't really properly published there it
makes sense to use version 1.0.0 and it shouldn't cause many probles since
most likely no one used the project. The version was set to 1.0.0.

The project used to use git tags for versioning when it was called
`better-json`. I renamed the tags so now they follow pattern
`better-json-<semver>-OLD`. The `<semver>` tags may be used in the future
for tagging versions of the package after renaming it to `better-json-tools`.

Since the project has been published on PyPI I don't intend to rename it
again. This was a weird thing to do from the beginning.