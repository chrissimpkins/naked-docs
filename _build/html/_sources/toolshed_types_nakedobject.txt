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
A ``NakedObject`` is a generic object that supports equality testing based upon the contents of its attributes.

.. py:class:: NakedObject([attribute_dictionary])

    A ``NakedObject`` is instantiated with an optional Python dictionary parameter.  If the parameter is included, the dictionary keys are mapped to ``NakedObject`` attributes and the corresponding dictionary values are used to define the attribute values.

    :param dictionary attribute_dictionary: (*optional*) a Python dictionary that is used to define the attributes of a new instance of a ``NakedObject``.  Key names are mapped to attribute names and their corresponding values are mapped to the attribute values.

    .. py:method:: equals(other_object)

        The ``equals()`` method performs equality testing between the NakedObject and another object.  Equality is defined by the equality of type ``type(NakedObject()) == type(other_object)`` and equality of attribute names and values ``NakedObject().__dict__ == other_object.__dict__``.  This equality test will therefore fail if the ``other_object`` parameter:

        * has a different type (e.g. comparison to a string type)
        * has fewer attributes
        * has more attributes
        * has the same number of attributes with different names
        * has the same number of attributes with the same names & different values
        * has the same number of attributes with the same names, same values, but values are of different types (e.g. '1' vs. 1)

        :param object other_object: a test object
        :returns: (boolean) ``True`` = the equality conditions are met; ``False`` = the equality conditions are not met

    .. note::

        The ``==`` and ``!=`` operators can be used in place of the ``equals()`` method and the negation of the ``equals()`` method, respectively.


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

**Determine Type of NakedObject**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})
    print(type(obj)) # prints <class 'Naked.toolshed.types.NakedObject'>

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

**Equality Testing of NakedObjects**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})
    obj2 = NakedObject({'example': 'an example string'})
    print(obj.equals(obj2)) # prints True
    print(obj == obj2) #prints True

**Equality Testing of NakedObjects, Failure on Different Attributes**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})
    obj2 = NakedObject({'different': 'an example string'})
    print(obj.equals(obj2)) # prints False
    print(obj == obj2) # prints False

**Equality Testing of NakedObjects, Failure on Different Attribute Values**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})
    obj2 = NakedObject({'example': 'different'})
    print(obj.equals(obj2)) # prints False
    print(obj == obj2) # prints False

**Equality Testing of NakedObjects, Failure on Different Attribute Number**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})
    obj2 = NakedObject({'example': 'an example string', 'example2': 'another string'})
    print(obj.equals(obj2)) # prints False
    print(obj == obj2) # prints False


**Equality Testing of NakedObject, Failure on Different Type**

.. code-block:: python

    from Naked.toolshed.types import NakedObject

    obj = NakedObject({'example': 'an example string'})
    obj2 = "an example string"
    print(obj.equals(obj2)) # prints False
    print(obj == obj2) # prints False


