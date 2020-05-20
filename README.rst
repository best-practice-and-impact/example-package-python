Example Package Python
======================

This is a simple python package, providing a template to write your own.

A package is a collection of code that aims to perform related tasks, or perform a high level function.
Python packages contain modules (``.py`` files) that can be grouped into any number of sub-packages (folders below the package folder).
This basic package contains a single module - `example_module` - and no sub-packages.

Package components are typically imported using one of the following methods:

.. code-block:: python

    import examplepackage

    examplepackage.example_module.example_function()


.. code-block:: python

    from examplepackage.example_module import example_function

    example_function()


See this `Real Python guide <https://realpython.com/python-modules-packages/>`_ for further information on importing packages and modules.


Setup
-----

There are two key components that distinguish a python packages from folders containing a collection of python files:

* ``__init__.py`` files
* ``setup.py``


``__init__.py``
^^^^^^^^^^^^^^^

An ``__init__.py`` file allows files (now modules) within the same directory to imported.
You should include one in each directory of your package that contains python code.

You will often find these files empty, but they do have an additional use.
Code within a ``__init__.py`` file is executed when the package or sub-package is imported.
Any objects defined in this file will therefore be available at that level of the package.
One use for this is importing useful modules, functions or classes from deep within your package stucture, making them accessible from the package level.

.. code-block:: python

    from examplepackage.example_module import example_function


With the code above included in the top-level ``__init__.py``, ``example_function`` can be accessed by users via simpler import statements:

.. code-block:: python

    import examplepackage
    
    examplepackage.another_function()


.. code-block:: python

    from examplepackage import another_function
    
    another_function()



``setup.py``
^^^^^^^^^^^^

This file sits outside of the folder containing your package code.
It contains the instructions that the ``setuptools`` library uses to build and install your package.
It includes:

* the name that users will use to import your package (lower case with no spaces, hyphens or underscores)
* author and/or maintainer contact details
* the folders to install, or use ``setuptools.find_packages()`` to do this for you.
* ``install_requires`` - other packages that this package depends on
* classifiers that describe the required major python version and operating system - this is necessary for uploading a package to PyPI


Installing your package
-----------------------

Packages can only be imported if they are located in a directory on the system path (``sys.path``).

Package installed using ``pip`` are located on the system path.
You can install local packages that you are working on in develop mode, by pointing pip the directory that contains ``setup.py`` and your package folder:

.. code-block:: command

    pip install -e local_path/example-package-python

This creates a reference to your local package files - you'll see a ``.egg-info`` file has been created next to your package.

Be sure to uninstall your package once you've finished- don't just delete the ``.egg-info`` reference.
Use the name of the package, like so:

.. code-block:: command

    pip uninstall examplepackage


Documentation
-------------

A README is a good place to provide an overview of your package or project.
This README is written in reStructuredText (``.rst``) for easy integration with the main documentation (`/docs`).
However, Markdown and many other markup languages work just as well.

The `sphinx package <https://www.sphinx-doc.org/en/master/usage/quickstart.html>`_ is very useful for generating detailed package documentation, and can generate this from inline documentation in your code.
Documentation usually sits inside the package, in a `docs/` folder.


Dependencies
------------

Listing your package depencencies ensures that your package works.
Explicitly stating versions of dependencies can increase the reproducibility of outputs from your package that depend on other packages.

Python package dependencies can indicate minimum package versions (``>=``) or the exact version number (``==``) that is required.

.. code-block:: txt

    pandas==1.0.0
    numpy>=1.18.4


License
-------

It's important to let users and developers know under what circumstance they can use, modify and redistribute your code.

The ``LICENSE`` file associated with your package should contain the text for the packages license.
The example in this package is for the MIT license.


Versioning
----------

A version number is essential for releasing your package.
`Semantic versioning <https://semver.org/>`_ is an useful method for informative versioning.

It can be useful to store this in a separate file, so that it can be referenced from multiple places (e.g. ``setup.py`` and the main documentation).


Including Other Files
---------------------

You may want to include example data or other non-python files in your package.
Be aware that the documentation for including non-python files is `notoriously bad <https://stackoverflow.com/a/14159430/8103477>`_, as most methods have been depreciated.

To include data in your source and binary distributions:

* In the ``setup.py`` file ``setup(...)``` function call, include ``include_package_data = True``.
* Alongside your `setup.py` file, provide a `MANIFEST.in` file.

This should list any non-python files that you wish to include.

A ``MANIFEST.in`` file includes single files, or all files of a type, as below:

.. code-block:: txt

    include README.rst
    recursive-include examplepackage/examples *.csv


Distributing
------------

Storing your source code in an open repository allows others to view and critique your code.

To allow others to install and use your code more easily, consider uploading your package to the Python Package Index (PyPI).
PyPI is an online repository of python packages.
It is the default repository used by pip.

Please see this `in-depth guide to packaging projects <https://packaging.python.org/tutorials/packaging-projects/>`_ for instructions on uploading your package to PyPI.
