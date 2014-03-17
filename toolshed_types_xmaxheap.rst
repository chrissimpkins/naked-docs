Toolshed: ``types`` : ``XMaxHeap``
===================================

.. py:module:: Naked.toolshed.types

Import ``XMaxHeap``
^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    from Naked.toolshed.types import XMaxHeap


Import ``XMaxHeap`` from C Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    from Naked.toolshed.c.types import XMaxHeap

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The ``XMaxHeap`` class is a max heap priority queue that extends Python ``heapq``.  This class supports sorting of new items that are pushed to the queue by assigned priority and pop of the highest priority item (in contrast to the Python built-in heapq which returns the lowest priority item).  It also supports the addition of attribute metadata on instantiation of the class.

.. py:class:: XMaxHeap([attribute_dictionary])

	:param dict attribute_dictionary: (*optional*) a Python dictionary that is used to define the attributes of a new instance of a ``XMaxHeap``.  Key names are mapped to attribute names and their corresponding values are mapped to the attribute values.

	**Function Overload**

	.. py:method:: __len__()

		:returns: (*int*) returns the number of items in the ``XMaxHeap``.  This allows you to use ``len(XMaxHeap())`` to determine the number of items in the priority queue.

	**XMaxHeap Methods**

	.. py:method:: length()

		:returns: (*int*) returns the number of items in the ``XMaxHeap``

	.. py:method:: pop()

		Pops the highest priority item off of the queue.

		:returns: (*item type dependent*) returns the highest priority item which is defined as the item that has the highest ``item_priority`` value.  If multiple items have the same value, they are returned on a first-in, first-out order (FIFO).

	.. py:method:: push(queue_item, item_priority)

		Pushes an item to the queue with the priority defined

		:param any queue_item: an object that is added to the priority queue.
		:param int item_priority: an integer that represents the priority of the item from 1 (min) to x (max).  It is possible to assign the same priority level to multiple items in the queue.

	.. py:method:: pushpop(queue_item, item_priority)

		Pushes an item to the queue and immediately pops and returns the highest priority item off of the queue.

		:param any queue_item: an object that is added to the priority queue.

		:param int item_priority: an integer that represents the priority of the item from 1 (min) to x (max).  It is possible to assign the same priority level to multiple items in the queue.

		:returns: (*item type dependent*) returns the highest priority item which is defined as the item that has the highest ``item_priority`` value.  If multiple items have the same value, they are returned on a first-in, first-out order (FIFO).  If the item that is pushed to the queue is the highest priority item, it is immediately returned.



