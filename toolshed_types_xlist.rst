Toolshed: ``types`` : ``XList``
==================================

.. py:module:: Naked.toolshed.types

Import ``XList``
^^^^^^^^^^^^^^^^^^
.. code-block:: python

    from Naked.toolshed.types import XList

Import ``XList`` from C Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    from Naked.toolshed.c.types import XList

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The ``XList`` class is an extension of the Python list type.  You can use all built-in Python list methods with it.  It extends the built-in Python list type with operator overloads, metadata definitions on instantiation, preservation of metadata on conversion to other types (with included XList methods), and a number of additional list methods.

The ``XList`` supports equality testing based upon **both** the values of the list items as well as the supplemental XList metadata (if included).  You can use the ``==`` and ``!=`` operators to perform this testing (or alternatively, the :meth:`XList.equals` method).

.. py:class:: XList(the_list, [attribute_dictionary])

    A ``XList`` is instantiated with any Python sequence type, including sets, tuples, and other lists.  You have the option to include a Python dictionary as a second parameter to include additional metadata.  The metadata are stored as attributes on the ``XList`` with dictionary keys mapped to attribute names and dictionary values mapped to the corresponding attribute values.

    :param list the_list: the data that are used to create an instance of a ``XList`` list.  This can be of any Python sequence type, including sets, tuples, and other lists.
    :param dictionary attribute_dictionary: (*optional*) a Python dictionary that is used to define the attributes of a new instance of a ``XList``.  Key names are mapped to attribute names and their corresponding values are mapped to the attribute values.

    **Overloaded Operators**

    .. py:method:: __add__(*other_lists)

    	The ``+`` operator is overloaded to extend the ``XList`` with one or more other ``XLists`` or lists.  The ``XList`` must be the left sided operand in your statement to use this overloaded operator.  When used with a Python list, the ``XList`` is extended with the items in the list.  When used with another ``XList``, the original ``XList`` is extended with the items *and the attributes* in the other ``XList``.  The right sided ``XList`` operand attribute values take precendence when the same attribute is included in both ``XLists``.

    	:param list other_lists: one or more Python lists or ``XList`` (i.e. can add multiple XLists: xl = xl1 + xl2 + xl3)
        :returns: (*XList*) returns the original XList extended with data in the ``*other_lists`` as defined above

    .. py:method:: __iadd__(other_list)

    	The ``+=`` operator is overloaded to extend the ``XList`` with another ``XList`` or list.  The ``XList`` must be the left sided operand in your statement to use this overloaded operator.  When used with a Python list, the ``XList`` is extended with the items in the list.  When used with another ``XList``, the original ``XList`` is extended with the items *and the attributes* in the other ``XList``.  The right sided ``XList`` operand attribute values take precendence when the same attribute is included in both ``XLists``.

    	:param list other_list: a Python list or ``XList``
    	:returns: (*XList*) returns the original XList extended with data in the ``other_list`` as defined above

    .. py:method:: __eq__(other_list)

        The ``==`` operator is overloaded to perform equality testing as defined for the :meth:`equals` method below.

        :returns: (*boolean*) ``True`` = conditions for equality are met; ``False`` = conditions for equality are not met

    .. py:method:: __neq__(other_dictionary)

        The ``!=`` operator is overloaded to return the negation of the test for equality as it is defined in the :meth:`equals` method below.

        :returns: (*boolean*) ``True`` = conditions for equality are not met; ``False`` = conditions for equality are met


    **XList Methods**

    .. py:method:: conditional_map_to_items(conditional_func, map_func)

        Map a function ``map_func`` to items in a ``XList`` that meet a ``True`` condition in the function, ``conditional_func``.  See :meth:`map_to_items` if you would like to map a function to every item in the list.

        :param function conditional_func: a function that returns a boolean value where ``True`` means that the ``map_func`` should be executed on the item
        :param function map_func:  the function that is conditionally executed with the ``XList`` item as a parameter.  The return value is used as the replacement value in the ``XList``.  If the function does not return a value, the item is replaced with ``None``.

    .. py:method: count_ci(test_string)

        Count the number of case-insensitive ``test_string`` strings that are included in the ``XList`` items.  This function can be used with a ``XList`` that includes both string and non-string types.

        :param string test_string: the string that is used for the case-insensitive match attempt
        :returns: (*int*) returns an integer count

    .. py:method:: count_duplicates()

        Count the number of duplicate items in the ``XList``. See :meth:`remove_duplicates` to remove the duplicated items.

        :returns: (*int*) returns the count of duplicate items

    .. py:method:: difference(test_list)

        Return a set with the items in the ``XList`` that are not contained in the parameter ``test_list``.  Also see :meth:`intersection`.

        :param list test_list: a ``XList`` or list that is to be tested against
        :returns: (*set*) returns a Python set

    .. py:method:: equals(other_object)

        The ``equals()`` method performs equality testing between a ``XList`` and another object.  The ``==`` operator can also be used to perform this test between the left (``XList``) and right (``other_object``) sided operands.  Equality testing is defined by meeting the criteria: (1) the type of the ``XList`` and the ``other_object`` are the same; (2) the list item values in the ``XList`` and the ``other_object`` are the same; (3) the attribute metadata (if present) are the same in the ``XList`` and the ``other_object``.

        :param object other_object: an object that is to be tested for equality
        :returns: (*boolean*) ``True`` = conditions for equality are met; ``False`` = conditions for equality are not met

    .. py:method:: intersection(test_list)

        Return a set with the items in ``XList`` that are also contained in the parameter ``test_list``. Also see :meth:`difference`.

        :param list test_list: a ``XList`` or list that is to be tested against
        :returns: (*set*) returns a Python set

    .. py:method:: join(delimiter)

    	Joins the string items in a ``XList`` with the ``delimiter`` string between each ``XList`` item and returns a string (or unicode) type.

    	:param string delimiter: the character or string to use as the delimiter between the items in the ``XList`` that are joined
    	:returns: (*string*) returns a string or unicode type depending upon the types of the ``XList`` items, the ``delimiter`` character or string, and the Python interpreter version.

    .. py:method:: map_to_items(map_func)

        Map a function to every item in the ``XList``.  To conditionally map a function to ``XList`` items (based upon conditions in a second function), see :meth:`conditional_map_to_items`.

        :param function map_func: the function that will take each item as a parameter and return the value for the replacement in the ``XList``
        :returns: item and function dependent type.  Items will be assigned a value of ``None`` if there is no return value from the function

    .. py:method:: max()

        Returns the maximum item value in the ``XList``.  Also see :meth:`min`.

        :returns: numeric type, dependent upon the type of the ``XList`` items

    .. py:method:: min()

        Returns the minimum item value in the ``XList``. Also see :meth:`max`.

        :returns: numeric type, dependent upon the type of the ``XList`` items

    .. py:method:: postfix(after_string)

        Appends a character or string suffix to each item in the ``XList``.  Also see :meth:`prefix` and :meth:`surround`.

        :param string after_string: the character or string to append to each ``XList`` item
        :returns: (*XList*) returns a ``XList`` with the above modification to each item

    .. py:method:: prefix(before_string)

        Prefixes a character or string to each item in the ``XList``.  Also see :meth:`postfix` and :meth:`surround`.

        :param string before_string: the character or string to prefix on each item in the ``XList``
        :returns: (*XList*) returns a ``XList`` with the above modification to each item

    .. py:method:: random()

        Return a random item from the ``XList``.  The random selection is performed with the Python random.choice() method.

        :returns: random item from the ``XList``

    .. py:method:: random_sample(number_items)

        Return a random sample of items from the ``XList``.  The number of items in the sample is defined with the ``number_items`` parameter.  Random sampling is performed without replacement.

        :param integer number_items: the number of items to include in the sample
        :returns: (*list*) returns a Python list containing ``number_items`` randomly sampled items from the ``XList``.

    .. py:method:: remove_duplicates()

        Removes the duplicate items in a ``XList`` and returns the ``XList``.  See :meth:`count_duplicates` for duplicate counts.

        :returns: (*XList*) returns the modified ``XList`` with duplicates removed

    .. py:method:: shuffle()

        Randomly shuffles the position of the items in the ``XList``

        :returns: (*XList*) returns a ``XList`` with the above modification

    .. py:method:: sum()

        Returns the sum of the item values in the ``XList``.  Not defined for non-numeric types.

        :returns: numeric type, dependent upon the type of the ``XList`` items

    .. py:method:: surround(first_string [, second_string])

        Perform prefix and suffix string concatenation to every item in a ``XList``.  Also see :meth:`prefix` and :meth:`postfix`.

        :param string first_string: character or string that is concatenated to the beginning of each ``XList`` item.  If ``second_string`` is not specified, this character or string is also concatentated to the end of each ``XList`` item.
        :param string second_string: (*optional*) optional second character or string parameter that is appended to each ``XList`` item.  If it is not specified, the ``first_string`` is concatenated to the beginning and end of each ``XList`` item.
        :returns: (*XList*) returns a ``XList`` with the above modifications to each item

    .. py:method:: wildcard_match(wildcard)

        Match items in the ``XList`` by wildcard value and return a list that contains the matched items.

        :param string wildcard: the wildcard value that is to be used for the match attempt
        :returns: (*list*) Python list containing the matched items.  If there are no matched items, an empty list is returned.
        :raises: ``TypeError`` if the ``XList`` contains non-string items

    .. py:method:: multi_wildcard_match(wildcard_sequence)

        Match items in the ``XList`` against more than one wildcard.  Items are included in the returned list if they match any of the included wildcards.

        :param string wildcard_sequence: a sequence of wildcards delimited by the ``|`` character (e.g. '*.py|*.pyc')
        :returns: (*list*) Python list containing the matched items.  If there are no matched items, an empty list is returned.
        :raises: ``TypeError`` if the ``XList`` contains non-string items

    **XList Cast Methods**

    .. py:method:: xset()

        Cast a ``XList`` to a ``XSet``.

        :returns: (*XSet*) returns a ``XSet`` with preservation of metadata

    .. py:method:: xfset()

        Cast a ``XList`` to a ``XFSet``.

        :returns: (*XFSet*) returns a ``XFSet`` with preservation of metadata

    .. py:method:: xtuple()

        Cast a ``XList`` to a ``XTuple``.

        :returns: (*XTuple*) returns a ``XTuple`` with preservation of metadata


Examples
^^^^^^^^^^

**Create a New Instance of XList, No Metadata**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'])

**Create a New Instance of XList, With Metadata**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'], {'listtype': 'orderlist'})

**Access XList Item**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'], {'listtype': 'orderlist'})
    print(xl[0]) # prints 'first'

**Access XList Attribute**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'], {'listtype': 'orderlist'})
    print(xl.listtype) # prints 'orderlist'

**Compare XList, Different List Items**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'], {'type': 'orderlist'})
    xl2 = XList(['different', 'second', 'third'], {'type': 'orderlist'})
    print(xl == xl2) # prints False

**Compare XList, Different Attribute Metadata**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'], {'type': 'orderlist'})
    xl2 = XList(['first', 'second', 'third'], {'type': 'another_orderlist'})
    print(xl == xl2) # prints False

**Extend the XList with Another List**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'], {'type': 'orderlist'})
    a_list = ['fourth', 'fifth']
    xl2 = xl + a_list
    print(xl2) # prints ['first', 'second', 'third', 'fourth', 'fifth']
    print(xl2.type) # prints 'orderlist'

**Extend the XList with Another List, Alternate Approach with += Overload**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'], {'type': 'orderlist'})
    a_list = ['fourth', 'fifth']
    xl += a_list
    print(xl) # prints ['first', 'second', 'third', 'fourth', 'fifth']
    print(xl.type) # prints 'orderlist'

**Comma Delimited String from XList**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'], {'type': 'orderlist'})
    cd_string = xl.join(',')
    print(cd_string) # prints 'first,second,third'

**Wrap with Quotes**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['first', 'second', 'third'], {'type': 'orderlist'})
    quote_list = xl.surround('"')
    print(quote_list) # prints ['"first"', '"second"', '"third"']

**Wrap with HTML Tags**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['paragraph one', 'paragraph two', 'paragraph three'], {'type': 'orderlist'})
    tag_list = xl.surround('<p class="naked">', '</p>')
    for x in tag_list:
        print(x)

    # prints:
    #  '<p class="naked">paragraph one</p>'
    #  '<p class="naked">paragraph two</p>'
    #  '<p class="naked">paragraph three</p>'

**Conditional Mapping of a Function to XList Items**

.. code-block:: python

    from Naked.toolshed.types import XList

    def true_a(xlist_item):
            return xlist_item.startswith('a')

    def cap_val(xlist_item):
        return xlist_item.upper()

    xl = XList(['another', 'one', 'many'], {'type': 'orderlist'})
    new_list = xl.conditional_map_to_items(true_a, cap_val)
    print(new_list)  # prints ['ANOTHER', 'one', 'many']

**Multiple Wildcard Match**

.. code-block:: python

    from Naked.toolshed.types import XList

    xl = XList(['one', 'two', 'three'], {'type': 'orderlist'})
    print(xl.multi_wildcard_match('o*|*hre*')) # prints ['one', 'three']



