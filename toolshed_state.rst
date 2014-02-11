Toolshed: ``state``
======================

.. py:module:: Naked.toolshed.state

Import State Module
^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.state


Import State C Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.c.cstate

.. note::

    Note the difference in the name of the C source module ``cstate`` relative to other toolshed module imports which follow the same naming scheme as the standard Python version.

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The state module has a single class, the :py:class:`StateObject`.  This is an object that generates and maintains user state data that is current as of the time of the :py:class:`StateObject` instantation.

Classes
^^^^^^^^

.. py:class:: StateObject()

    The StateObject is instantiated without parameters.  Attributes can be accessed with standard Python dot syntax following instantiation (e.g. ``state.py2``).

    **Attributes**:

    .. py:attribute:: cwd

        (*string*) User current working directory (from Python ``os.getcwd()``)

    .. py:attribute:: day

        (*int*) Local day of the calendar month (from ``datetime.datetime.now().day``)

    .. py:attribute:: default_path

        (*string*) Default user PATH string (from Python ``os.defpath``)

    .. py:attribute:: file_encoding

        (*string*) User system default file encoding (from Python ``sys.getfilesystemencoding()``)

    .. py:attribute:: hour

        (*int*) Local system hour of the day [24hr format] (from Python ``datetime.datetime.now().hour``)

    .. py:attribute:: min

        (*int*) Local system minute of the day (from Python ``datetime.datetime.now().minute``)

    .. py:attribute:: month

        (*int*) Local system month of the year (from Python ``datetime.datetime.now().month``)

    .. py:attribute:: os

        (*string*) User operating system (from Python ``sys.platform``)

    .. py:attribute:: parent_dir

        (*string*) User parent directory relative to current working directory (from Python ``os.pardir``)

    .. py:attribute:: py2

        (*boolean*) Truth test for Python 2 interpreter executing script on user system (test derived from Python ``sys.version_info``)

    .. py:attribute:: py3

        (*boolean*) Truth test for Python 3 interpreter executing script on user system (test derived from Python ``sys.version_info``)

    .. py:attribute:: py_major

        (*int*) The Python major version - **2** .7.6 - (from Python ``sys.version_info``)

    .. py:attribute:: py_minor

        (*int*) The Python minor version - 2. **7** .6 - (from Python ``sys.version_info``)

    .. py:attribute:: py_patch

        (*int*) The Python patch version - 2.7. **6** - (from Python ``sys.version_info``)

    .. py:attribute:: second

        (*int*) Local system seconds of the current minute (from Python ``datetime.datetime.now().second``)

    .. py:attribute:: string_encoding

        (*string*) User system string encoding (from Python ``sys.getdefaultencoding()``)

    .. py:attribute:: user_path

        (*string*) User's USER directory path (from Python ``os.path.expanduser("~")``)

    .. py:attribute:: year

        (*int*) Local system year string (from Python ``datetime.datetime.now().year``)


Add Your Own Attributes to the StateObject
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you need to maintain additional information, simply add a new attribute to the StateObject:

.. code-block:: python

    from Naked.toolshed.state import StateObject

    state = StateObject()
    state.user_name = 'Guido'         # assign a new attribute
    state.fav_food = 'spam and eggs'  # assign a new attribute

    # do other things

    print(state.user_name)   # prints 'Guido'
    print(state.fav_food)    # prints 'spam and eggs'

There are no restrictions against overwriting an existing attribute in the StateObject if you would like to re-define it.

Examples
^^^^^^^^^^^
If you use ``naked make`` to generate your project, the :py:class:`StateObject` is instantiated as an instance named ``state`` in your ``app.py`` file.  If you create the instance of the StateObject in a different file, or implement this yourself in the ``app.py`` file, replace ``state`` in the following examples with the name of your instance.  You can access the :py:class:`StateObject` data with dot syntax.

**Python 2 vs. 3 Test**

.. code-block:: python

    if state.py2:
        # Python 2 code
    else:
        # Python 3 code

**Distinguish Python 2.6 from Python 2.7**

.. code-block:: python

    if state.py2:
        if state.py_minor == 6:
            # Python 2.6 code
        elif state.py_minor == 7:
            # Python 2.7 code

**Distinguish Python 3.2 from Python 3.3**

.. code-block:: python

    if state.py3:
        if state.py_minor == 2:
            # Python 3.2 code
        elif state.py_minor == 3:
            # Python 3.3 code

**Current Working Directory Lookup**

.. code-block:: python

    curr_dir = state.cwd
    # the current working directory path is now in `curr_dir`

**User Operating System**

.. code-block:: python

    opsys = state.os
    # opsys contains the operating system name - see Python sys.platform documentation for key

**Print the Date**

.. code-block:: python

    date_string = state.month + ' ' + state.day + ' ' + state.year
    print(date_string)

**Print the Time**

.. code-block:: python

    time_string = state.hour + ':' + state.min + ':' + state.second





