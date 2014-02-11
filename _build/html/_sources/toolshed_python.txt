Toolshed: ``python``
======================

.. py:module:: Naked.toolshed.python

Import Python Module
^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.state


Import Python C Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.c.python

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The python module provides functions for Python version testing.  It is used internally in the Naked Framework by the :py:class:`Naked.toolshed.state.StateObject`.  The functions are public if you would like to use them directly.


Classes
^^^^^^^^

None

Functions
^^^^^^^^^^^^

.. py:function:: is_py2()

	Truth test for execution of script with Python version 2 interpreter

	:rtype: boolean

.. py:function:: is_py3()

	Truth test for execution of script with Python version 3 interpreter

	:rtype: boolean

.. py:function:: py_version()

	Full Python version tuple.

	:rtype: tuple (major, minor, patch)

.. py:function:: py_major_version()

	The major version of the Python interpreter

	:rtype: int

.. py:function:: py_minor_version()

	The minor version of the Python interpreter

	:rtype: int

.. py:function:: py_patch_version()

	The patch version of the Python interpreter

	:rtype: int


