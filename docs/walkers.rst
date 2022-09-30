JSON Walkers
============
.. currentmodule:: better_json_tools.json_walker

Description
-----------

:class:`JSONWalker` and
:class:`JSONSplitWalker` classes let you navigate JSON
easier without a need to constantly handle exceptions. You can simply provide
full JSON path to the value you want and than check if it exists.

They use the syntax similar to pathlib Path objects, they overload the division
(`/`) and integer division (`//`) operators to create paths.

`/` is used to create simple paths, where the keys are either strings
(for accessing objects) or integers (for accesing arrays) or :class:`JSONPath`
objects which internally are just tuples of strings and integers representing
a longer path.

`//` is used to create split paths, when applied to a JSON walker, it creates
a JSON split walker, which has a list of JSON walkers representing all of the
matching paths. The arguments of this operations can be following:

- literal `str` - matches any key of the object
- literal `int` - matches any index of the array
- `None` - matches any key or index
- literal :class:`SKIP_LIST` - can be used to enter every item of an array, or
  if current value is an object, it returns that object. It's useful when
  the structure of the JSON file allows the item to be either an object or a
  list of objects.
- string values are interpreted as regular expressions, which are matched
  against the keys of the objects.

Code example
------------

.. code-block:: python

    from better_json_tools import JSONWalker

    with open('file.json', 'r') as f:
        walker = JSONWalker.load(f)

    # the content of the file
    print(walker.data)
    # output:
    # {'a': 1, 'b': [{'x': 1, 'y': 2}, {'x': 4, 'y': 5}],
    # 'c': {'c1': {'x': 11, 'y': 22}, 'c2': {'x': 44, 'y': 55}}}

    # the value of 'a' property
    print((walker / 'a').data)
    # output:
    # 1

    # the value of any list element from 'b' property
    for i in (walker / 'b' // int).data:
        print(i.data)
    # output:
    # {'x': 1, 'y': 2}
    # {'x': 4, 'y': 5}

    # the 'x' value of any item (from list or object) from any object that
    # matches the '[a-z]' regex
    for i in (walker // '[a-z]' // None / 'x').data:
        print(i.data)
    # output:
    # 1
    # 4
    # 11
    # 44

    # Creating JSON paths using create_path method
    data = JSONWalker({})

    new_path = data /'a' / 'b'
    new_path.create_path("Hello")
    # data:
    # {"a": {"b": "Hello"}}

    new_path = data / 'c' / 3
    new_path.create_path("Test", empty_list_item_factory=lambda: "abc")
    # data:
    # {"a": {"b": "Hello"}, "c": ["abc", "abc", "abc", "Test"]}

Classes
-------

.. autoclass:: JSONPath
   :members:

.. autoclass:: JSONWalker
   :members:
   :special-members: __truediv__, __floordiv__, __add__


.. autoclass:: JSONSplitWalker
   :members:
   :special-members: __truediv__, __floordiv__, __add__, __iter__
