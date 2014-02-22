Toolshed: ``types`` : ``NakedObject``
=======================================

.. py:module:: Naked.toolshed.types


Import ``NakedObject``
^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    from Naked.toolshed.types import NakedObject


Import ``NakedObject`` from C Source File
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    from Naked.toolshed.c.types import NakedObject

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
A ``NakedObject`` class is a generic object.

.. py:class:: NakedObject([attribute_dictionary])

    A ``NakedObject`` is instantiated with an optional Python dictionary parameter.  If the parameter is included, the dictionary keys are mapped to ``NakedObject`` attributes and the corresponding dictionary values are used to define the attribute values.

    :param dictionary attribute_dictionary: (*optional*) a Python dictionary that is used to define the attributes of a new instance of a ``NakedObject``.  Key names are mapped to attribute names and their corresponding values are mapped to the attribute values.

Examples
^^^^^^^^^^

**Create a New Instance of an Empty NakedObject**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject()

**Create a New Instance of a NakedObject with Attributes**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})

**Set New Attribute on NakedObject**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject()
    obj.example = 'an example string'

**Get Attribute Value from NakedObject**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})
    the_value = obj.example

**Delete Attribute from NakedObject**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})
    del obj.example

**Test for Existence of an Attribute**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})
    if hasattr(obj, 'example'):
        # do something with the attribute




