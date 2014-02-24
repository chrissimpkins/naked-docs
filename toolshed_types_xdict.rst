Toolshed: ``types`` : ``XDict``
==================================

.. py:module:: Naked.toolshed.types

Import ``XDict``
^^^^^^^^^^^^^^^^^^
.. code-block:: python

    from Naked.toolshed.types import XDict


Import ``XDict`` from C Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    from Naked.toolshed.c.types import XDict

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The ``XDict`` class is an extension of the Python dictionary type.  You can use all built-in Python dictionary methods with it.  It extends the built-in Python dictionary type with operator overloads, metadata definitions on instantiation, preservation of metadata on conversion to other types (with included XDict methods), and a number of additional dictionary methods.

The ``XDict`` supports equality testing based upon **both** the dictionary data as well as the supplemental metadata (if included).  You can use the ``==`` and ``!=`` operators to perform this testing (or alternatively, the :meth:`XDict.equals` method).

.. py:class:: XDict(the_dictionary, [attribute_dictionary])

    A ``XDict`` is instantiated with a Python dictionary.  You have the option to include a second Python dictionary to include additional metadata.  The metadata are stored as attributes on the ``XDict`` with dictionary keys mapped to attribute names and dictionary values mapped to the corresponding attribute values.

    :param dictionary the_dictionary: the data that are used to create an instance of a ``XDict`` dictionary.
    :param dictionary attribute_dictionary: (*optional*) a Python dictionary that is used to define the attributes of a new instance of a ``XDict``.  Key names are mapped to attribute names and their corresponding values are mapped to the attribute values.

    **Overloaded Operators**

    .. py:method:: __add__(other_dictionary)

        The ``+`` operator is overloaded to update the ``XDict`` with new key:value pairs from a Python dictionary or another ``XDict``.  An ``XDict`` must be the left sided operand in this statement as standard Python dictionaries do not support this form of dictionary combination.  When used with a Python dictionary, the key:value pairs in the Python dictionary are added to the ``XDict`` dictionary.  When used with another ``XDict``, the key:value pairs from the ``XDict`` parameter are defined in the ``XDict`` dictionary **and** the attributes from the ``XDict`` parameter are defined in the ``XDict``.  The parameter dictionary definitions take precedence for key:value and attributes on the returned ``XDict`` when both objects contain the same dictionary key or attribute name.

        :param dictionary other_dictionary: a Python dictionary or ``XDict``
        :returns: (*XDict*) returns the original XDict updated with data in the ``other_dictionary`` as defined above

    .. py:method:: __iadd__(other_dictionary)

        The ``+=`` operator is overloaded to update the ``XDict`` operand on the left side of the operator with the Python dictionary or ``XDict`` on the right side of the operator.  The update takes place as defined in the description of the :meth:`__add__` method above.

        :returns: (*XDict*) returns a ``XDict`` that is updated with the data in the right sided operand.

    .. py:method:: __eq__(other_dictionary)

        The ``==`` operator is overloaded to perform equality testing as defined for the :meth:`equals` method below.

        :returns: (*boolean*) ``True`` = conditions for equality are met; ``False`` = conditions for equality are not met

    .. py:method:: __neq__(other_dictionary)

        The ``!=`` operator is overloaded to return the negation of the test for equality as it is defined in the :meth:`equals` method below.

        :returns: (*boolean*) ``True`` = conditions for equality are not met; ``False`` = conditions for equality are met


    **Key Methods**

    .. py:method:: difference(other_dictionary)

        Returns the set of dictionary keys in the ``XDict`` that are not included in the ``other_dictionary`` parameter.

        :param dictionary other_dictionary: a Python dictionary or ``XDict``
        :returns: (*set*) Returns a set of dictionary key strings that meet this definition.  Returns an empty set if there are no keys that meet the definition.

    .. py:method:: intersection(other_dictionary)

        Returns the set of dictionary keys in the ``XDict`` that are also included in the ``other_dictionary`` parameter.

        :param dictionary other_dictionary: a Python dictionary or ``XDict``
        :returns: (*set*) Returns a set of dictionary key strings tha meet this definition.  Returns an empty set if there are no keys that meet the definition.

    .. py:method:: key_xlist()

        Returns a ``XList`` containing the keys in the ``XDict`` with preservation of the ``XDict`` attribute metadata in the returned ``XList``.

        :returns: (*XList*) returns a XList that contains the ``XDict`` keys mapped to list items.  The attribute data in the ``XDict`` is preserved in the returned ``XList``.


    **Value Methods**

    .. py:method:: conditional_map_to_vals(conditional_func, map_func)

        Map a function parameter ``map_func`` to every ``XDict`` value that has a **key** that returns ``True`` when the key is passed as a parameter to the ``conditional_func`` function.  Every ``XDict`` key is tested in the ``conditional_func``.

        :param function conditional_func: a function that accepts a ``XDict`` key as the first parameter and returns a boolean value.  When the returned value is ``True``, the value associated with this key is passed as the first parameter to the ``map_func``.

        :param function map_func: a function that accepts a ``XDict`` value as the first parameter and returns the object that will be used to update the value definition for the key in the returned ``XDict``.

        :returns: (*XDict*) returns the ``XDict`` with values that are updated as defined by the ``conditional_func`` and ``map_func`` processing.  If the ``map_func`` does not return a value, the associated key is defined with ``None``.  If you intend to maintain the original value, return the value that was passed as the parameter to the function.

    .. py:method:: map_to_vals(map_func)

        Maps a function parameter ``map_func`` to every value in the ``XDict``.  Every value in the ``XDict`` is passed to this function.

        :param function map_func: a function that accepts a ``XDict`` value and returns the object that will be used to update the value definition for the key in the returned ``XDict``
        :returns: (*XDict*) returns the ``XDict`` with values that are updated as defined by the returned values from the ``map_func``.  If the ``map_func`` does not return a value, the associated key is defined with ``None``.  If you intend to maintain the original value, return the value that was passed as the parameter to the function.

    .. py:method:: max_val()

        Returns a 2-item tuple containing the maximum value and associated key as defined by the Python built-in ``max()`` function.

        :returns: (*tuple*) returns a 2-item tuple that includes (``max value``, ``key``). The maximum numeric value is returned for numeric types.  The value at the top of the reverse alphabetic order is returned for strings.  For other types, the returned value is defined by the Python built-in ``max()`` function (if supported).

    .. py:method:: min_val()

        Returns a 2-item tuple containing the minimum value and associated key as defined by the Python built-in ``min()`` function.

        :returns: (*tuple*) returns a 2-item tuple that includes (``min value``, ``key``). The minimum numeric value is returned for numeric types.  The value at the top of the alphabetic order is returned for strings.  For other types, the returned value is as defined for the Python built-in ``max()`` function (if supported).

    .. py:method:: sum_vals()

        Returns the sum of the values as determined by the Python built-in ``sum()`` function.

        :returns: (*numeric*) returns the sum as a numeric type defined by the input types
        :raises: ``TypeError`` for unsupported operand types encountered as values in the ``XDict``

    .. py:method:: val_count(the_value)

        Returns the count of ``the_value`` values in the ``XDict``.  Values are counted if they meet the criterion ``XDict()[key] == the_value``.

        :param object the_value: the value type and definition to be counted in the ``XDict``
        :returns: (*integer*) returns the count of ``the_value`` in the ``XDict`` as an integer.

    .. py:method:: val_count_ci(the_value)

        Returns the count of a case-insensitive test for ``the_value`` string in the ``XDict`` values.  This method **can** be used with ``XDict`` that include value types that do not support the ``string.lower()`` method that is used in the case-insensitive testing.

        :param string the_value: the string value that is to be used for a case-insensitive count across all ``XDict`` values
        :returns: (*integer*) returns the count of strings that match ``the_value`` in a case-insensitive test.

    .. py:method:: val_xlist()

        Returns a ``XList`` that contains the ``XDict`` values mapped to list items.

        :returns: (*XList*) returns a ``XList`` that contains ``XDict`` values that are mapped to list items.  Any attribute metadata from the original ``XDict`` is maintained in the returned ``XList``.


    **Other Methods**

    .. py:method:: equals(other_object)

        The ``equals()`` method performs equality testing between a ``XDict`` and another object.  The ``==`` operator can also be used to perform this test between the left (``XDict``) and right (``other_object``) sided operands.  Equality testing is defined by meeting the criteria: (1) the type of the ``XDict`` and the ``other_object`` are the same; (2) the dictionary keys and values are the same in the ``XDict`` and the ``other_object``; (3) the attribute metadata (if present) are the same in the ``XDict`` and the ``other_object``.

        :param object other_object: an object that is to be tested for equality
        :returns: (*boolean*) ``True`` = conditions for equality are met; ``False`` = conditions for equality are not met

    .. py:method:: random()

        Returns a single, random key:value pair as a Python dictionary.  The random pair is identified with the Python ``random.sample()`` method.

        :returns: (*dictionary*) a Python dictionary that contains a single key:value pair

    .. py:method:: random_sample(number)

        Returns ``number`` random key:value pair(s) in a Python dictionary.  The random pairs are identified with the Python ``random.sample()`` method.  The random sampling is performed without replacement.

        :param integer number: the number of random key:value pairs to return
        :returns: (*dictionary*) a Python dictionary that contains ``number`` key:value pairs

    .. py:method:: xitems()

        A generator that yields 2-item tuples of key:value pairs from the ``XDict``.  This utilizes the ``dict.iteritems()`` generator when the Python 2 interpreter is used and the ``dict.items()`` generator when the Python 3 interpreter is used.

        :returns: (*tuple*) yields a 2-item tuple ``(key, value)`` on each iteration.  Iteration ends when all ``XDict`` key:value pairs have been returned.

    .. py:method:: type()

        Return the type of the ``XDict`` object.

        :returns: (type) returns the type of the ``XDict``


Examples
^^^^^^^^^^

**Create a New Instance of XDict, No Metadata**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd = XDict({'name': 'Guido', 'language': 'python'})


**Create a New Instance of XDict, With Metadata**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})

**Access XDict Value**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})
    print(xd['name']) # prints 'Guido'
    print(xd['language']) # prints 'python'

**Access XDict Attribute**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})
    print(xd.dict_type) # prints 'dev'

**Compare XDict, Different Dictionaries**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd1 = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})
    xd2 = XDict({'name': 'Yukihiro', 'language': 'ruby'}, {'dict_type': 'dev'})
    print(xd1 == xd2) # prints False
    print(xd != xd2) # prints True

**Compare XDict, Different Attributes**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd1 = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})
    xd2 = XDict({'name': 'Guido', 'language': 'python'}, {'rating': 1})
    print(xd1 == xd2) # prints False
    print(xd != xd2) # prints True

**Update XDict with Dictionary**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})
    py_dict = {'year': 1991}
    xd_with_year = xd + py_dict
    print(xd_with_year) # prints {'name': 'Guido', 'language': 'python', 'year': 1991}
    print(xd.dict_type) # prints 'dev'

**Update XDict with XDict**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd1 = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})
    xd2 = XDict({'year': 1991}, {'includes': 'year'})
    xd3 = xd1 + xd2
    print(xd3) # prints {'name': 'Guido', 'language': 'python', 'year': 1991}
    print(xd3.dict_type) # prints 'dev'
    print(xd3.includes) # prints 'year'

**Update XDict with XDict, Alternate Approach with += Overload**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd1 = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})
    xd2 = XDict({'year': 1991}, {'includes': 'year'})
    xd1 += xd2
    print(xd1) # prints {'name': 'Guido', 'language': 'python', 'year': 1991}
    print(xd1.dict_type) # prints 'dev'
    print(xd1.includes) # prints 'year'

**Make XList from XDict Keys**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})
    xl = xd.key_xlist()
    print(xl) # prints ['name', 'language']
    print(xl.dict_type) # prints 'dev'

**Make XList from XDict Values**

.. code-block:: python

    from Naked.toolshed.types import XDict

    xd = XDict({'name': 'Guido', 'language': 'python'}, {'dict_type': 'dev'})
    xl = xd.val_xlist()
    print(xl) # prints ['Guido', 'python']
    print(xl.dict_type) # prints 'dev'

**Conditional Mapping of a Function to XDict Values**

.. code-block:: python

    from Naked.toolshed.types import XDict

    def spam_corrector(the_argument):
        if the_argument == 'eggs':
            pass
        else:
            return 'eggs'

    def comp_detector(the_argument):
        if the_argument == 'complements':
            return True
        else:
            return False


    xd = XDict({'food': 'spam', 'complements': 'sausage'})
    xd = xd.conditional_map_to_vals(comp_detector, spam_corrector)
    print(xd) # prints {'food': 'spam', 'complements': 'eggs'}


