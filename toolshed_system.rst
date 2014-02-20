Toolshed: ``system``
========================

.. py:module:: Naked.toolshed.system


Import System Module
^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.system


Import System C Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.c.system

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The ``system`` module includes functions for file and directory paths, file and directory testing, file extension testing, file listings, file filters, file metadata, and decorators that insert file paths into function and method parameters. It also includes functions for simple printing to the standard output and standard error streams with exit code handling.

File I/O methods are available in the ``Naked.toolshed.file`` and ``Naked.toolshed.c.file`` modules.  Additional information is available in the :doc:`toolshed_file` documentation.


File and Directory Path Functions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: cwd()

    Returns the current working directory path.

    :returns: (string) current working directory path

.. py:function:: directory(file_path)

    Returns the directory path to the file in ``file_path``.

    :param string file_path: the absolute or relative file path to a file
    :returns: (string) the directory path that contains the file in ``file_path``

.. py:function:: file_extension(file_path)

    Returns the file extension from a file path.

    :param string file_path: the absolute or relative file path to a file
    :returns: (string) the file extension, including the period character

.. py:function:: filename(file_path)

    Returns the base filename from an absolute ``file_path``.

    :param string file_path: the absolute or relative file path to a file
    :returns: (string) base file name including the file extension

.. py:function:: fullpath(file_name)

    Returns the absolute path to a file that is in the current working directory, including the basename of the file.

    :param string file_name: the name of a file in the current working directory
    :returns: (string) the absolute path to a file that is in the current working directory

.. py:function:: make_path(*path_strings)

    Returns the OS independent file path from path component parameters

    :param string *path_strings: tuple of path component strings

    .. code-block:: python

        from Naked.toolshed.system import make_path

        file_path = make_path('user', 'guido', 'python', 'file.txt')

    :returns: (string) the OS independent path from the path component parameters in ``*path_strings``

:ref:`file-directory-path-examples` are available below.


File Path Decorators
^^^^^^^^^^^^^^^^^^^^^

.. py:decorator:: currentdir_to_basefile()

    Concatenates the absolute working directory path (*string*) to the basename of a file in the first parameter of the decorated function

.. py:decorator:: currentdir_firstparam()

    Adds the current working directory path (*string*) as the first parameter of the decorated function

.. py:decorator:: currentdir_lastparam()

    Adds the current working directory (*string*) as the last parameter of the decorated function

:ref:`file-path-decorator-examples` are available below.


File and Directory Testing Functions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: dir_exists(dir_path)

    Test for the existence of a directory at the path ``dir_path``.  This function confirms that the path is a directory and not a symbolic link or file.

    :param string dir_path: the path to be tested for the presence of a directory
    :returns: (boolean) ``True`` = directory exists at ``dir_path``; ``False`` = directory does not exist at ``dir_path``

.. py:function:: file_exists(file_path)

    Test for the existence of a file at the path ``file_path``.  This function confirms that the path is a file and not a symbolic link or directory.

    :param string file_path: the path to be tested for the presence of a file
    :returns: (boolean) ``True`` = file exists at ``file_path``; ``False`` = file does not exist at ``file_path``

.. py:function:: is_file(file_path)

    Test whether a path resolves to an existing file.

    :param string file_path: the path to be tested for a file
    :returns: (boolean) ``True`` = the ``file_path`` path is a file; ``False`` = the ``file_path`` path is not a file

.. py:function:: is_dir(dir_path)

    Test whether a path resolves to an existing directory.

    :param string dir_path: the path to be tested for a directory
    :returns: (boolean) ``True`` = the ``dir_path`` path is a directory; ``False`` = the ``dir_path`` path is not a directory

:ref:`file-directory-testing-examples` are available below.

File Metadata Functions
^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: file_size(file_path)

    Returns the size of the file at ``file_path`` in bytes.

    :param string file_path: the path to the file
    :returns: (integer) the size of the file in bytes

.. py:function:: file_mod_time(file_path)

    Returns the date and time of the last file modification

    :param string file_path: the path to the file
    :returns: (string) The date and time of the last file modification with the format ``'Wed Jan 29 23:49:04 2014'``.

:ref:`file-metadata-examples` are available below.

File Listings Functions
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: list_all_files(dir_path)

    List all files in the path ``dir_path``.

    :param string dir_path: the directory path containing the files of interest
    :returns: (list) Python list with each file path in ``dir_path`` mapped to a list item

.. py:function:: list_all_files_cwd()

    List all files in the current working directory.

    :returns: (list) Python list with each file path in the current working directory mapped to a list item

.. py:function:: list_filter_files(extension_filter, dir_path)

    List all files in the path ``dir_path`` that match the file extension filter ``extension_filter``.  Takes a file extension with or without the associated period character (e.g. ``.py`` or ``py``).

    :param string extension_filter: the file extension filter to be used for file selection
    :param string dir_path: the directory path containing the files of interest
    :returns: (list) Python list with each matching file path in ``dir_path`` mapped to a list item

.. py:function:: list_filter_files_cwd(extension_filter)

    List all files in the current working directory that match the file extension filter ``extension_filter``.  Takes a file extension with or without the associated period character (e.g. ``.py`` or ``py``).

    :param string extension_filter: the file extension filter to be used for file selection
    :returns: (list) Python list with each matching file path in current working directory mapped to a list item

.. py:function:: list_match_pattern(match_pattern)

    List all files that match a wildcard ``match_pattern`` parameter.

    :param string match_pattern: the wildcard match pattern (e.g. ``'/test/*.py'``)
    :returns: (list) Python list with each matching file path mapped to a list item

:ref:`file-listings-examples` are available below.


Directory Write Function
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: make_dirs(directory_path)

    Writes a new directory path to disk *if it does not already exist*.  This function does not overwrite an existing directory path.  Will perform a recursive directory tree write for multi-level directory structures.  Returns ``True`` if the directory write is successful.  Returns ``False`` if the directory write does not occur (e.g. requested directory already exists).

    :param string directory_path: the directory path to be written to disk
    :returns: (boolean) ``True`` = successful directory path write; ``False`` = unsuccessful directory path write

:ref:`make-directory-examples` are available below.


Symbolic Link Functions
^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: is_link(link_path)

    Test for the presence of a symbolic link at ``link_path``.

    :param string link_path: the path to test for the presence of a symbolic link
    :returns: (boolean) ``True`` = the path ``link_path`` is a symbolic link; ``False`` = the path ``link_path`` is not a symbolic link

.. py:function:: real_path(link_path)

    Return the real file path pointed to by the path ``link_path``.

    :param string link_path: the symbolic link path
    :returns: (string) the real file path pointed to by the symbolic link ``link_path``


Data Stream Functions
^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: stdout(text)

    Print the ``text`` string to the standard output stream with a newline character appended to the ``text`` string.  Identical to the Python ``print()`` function.

    :param string text: the string that will be printed to the standard output stream

.. py:function:: stdout_iter(iter)

    Print the items in an iterable object (``iter``) to the standard output stream *with* a newline after each item.

    :param object iter: An iterable object type in which all of the iterable items provide support for either the ``__str__`` or ``__repr__`` functions.

.. py:function:: stdout_iter_xnl(iter)

    Print the items in an iterable object (``iter``) to the standard output stream *without* a newline character after each item.  This prints the items in sequence on the same line of output.

    :param object iter: An iterable object type in which all of the iterable items provide support for either the ``__str__`` or ``__repr__`` functions.

.. py:function:: stdout_xnl(text)

    Print the ``text`` string to the standard output stream *without* a newline character appended to the ``text`` string.

    :param string text: the string that will be printed to the standard output stream

.. py:function:: stderr(text [, exit])

    Print the ``text`` string to the standard error stream with an optional non-zero exit status code.  A newline character is appended to the ``text`` string.  For non-zero ``exit`` integers, ``SystemExit()`` is raised with the exit status code.  ``SystemExit()`` is not raised by default (or if ``exit`` is assigned a value of 0).

    :param string text: the string that will be printed to the standard error stream
    :param integer exit: (*optional*) the exit status code

.. py:function:: stderr_xnl(text [, exit])

    Print the ``text`` string to the standard error stream with an optional non-zero exit status code.  This function does not append a newline character to the end of the ``text`` string before printing it to the standard error stream.  If the exit status code is changed to a non-zero integer, ``SystemExit()`` is raised with the exit status code.  ``SystemExit()`` is not raised by default (or if ``exit`` is assigned a value of 0).

    :param string text: the string that will be printed to the standard error stream
    :param integer exit: (*optional*) the exit status code

:ref:`data-stream-examples` are available below.


Application Exit Functions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: exit_failure()

    Exit the application with exit status code 1.

.. py:function:: exit_success()

    Exit the application with exit status code 0.

.. py:function:: exit_with_status(exit_code)

    Exit the application with exit status code ``exit_code``.

    :param integer exit_code: the exit status code. By default, an exit status code of 0 is used.


:ref:`application-exit-examples` are available below.


.. _file-directory-path-examples:

File and Directory Path Examples
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Current Working Directory**

.. code-block:: python

    from Naked.toolshed.system import cwd

    curr_dir = cwd()

**Make OS Independent Path String**

.. code-block:: python

    from Naked.toolshed.system import make_path

    file_path = make_path('path', 'to', 'test.txt')
    print(file_path) # prints path with OS dependent path delimiters

**Directory Path to File**

.. code-block:: python

    from Naked.toolshed.system import directory, make_path

    filepath = make_path('path', 'to', 'test.txt')
    dir_path = directory(dir_path)
    print(dir_path) # prints '/path/to/' with OS dependent delimiters

**File Extension**

.. code-block:: python

    from Naked.toolshed.system import file_extension, make_path

    file_path = make_path('path', 'to', 'test.txt')
    extension = file_extension(file_path)
    print(extension) # prints '.txt'

**Filename**

.. code-block:: python

    from Naked.toolshed.system import filename, make_path

    file_path = make_path('path', 'to', 'test.txt')
    file_name = filename(file_path)
    print(file_name) # prints 'test.txt'

**Absolute File Path**

.. code-block:: python

    from Naked.toolshed.system import fullpath, make_path

    # file /usr/c/test/test.txt & current working directory is /usr/c/test/
    absolute_path = fullpath('test.txt')
    print(absolute_path) # prints '/usr/c/test/test.txt' with OS dependent delimiters


.. _file-path-decorator-examples:

File Path Decorator Examples
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Current Working Directory Path Concatenation to First Parameter**

.. code-block:: python

    from Naked.toolshed.system import currentdir_to_basefile

    @currentdir_to_basefile
    def tester(path):
        print(path)

    # when run as tester('test.txt') from /usr/c/test/, prints '/usr/c/test/test.txt' with OS dependent delimiters

**Current Working Directory Path as First Parameter**

.. code-block:: python

    from Naked.toolshed.system import currentdir_firstparam

    @currentdir_firstparam
    def tester(path=''):
        print(path)

    # when run as tester() from /usr/c/test/, prints '/usr/c/test/' with OS dependent delimiters

**Current Working Directory Path as Last Parameter**

.. code-block:: python

    from Naked.toolshed.system import currentdir_lastparam

    @currentdir_lastparam
    def tester(file_name, dir_path=''):
        print(dir_path + file_name)

    # when run as tester('test.txt') from /usr/c/test/, prints '/usr/c/test/test.txt' with OS dependent delimiters


.. _file-directory-testing-examples:

File and Directory Testing Examples
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Directory Testing**

.. code-block:: python

    from Naked.toolshed.system import dir_exists, make_path

    # /usr/c/test does exist

    dir_path = make_path('usr', 'c', 'test')
    if dir_exists(dir_path):
        print('yep')  # prints 'yep'

**File Testing**

.. code-block:: python

    from Naked.toolshed.system import file_exists, make_path

    # /usr/c/test/test.txt exists

    file_path = make_path('usr', 'c', 'test', 'test.txt')
    if file_exists('/usr/c/test/test.txt'):
        print('yep') # prints yep


.. _file-metadata-examples:

File Metadata Examples
^^^^^^^^^^^^^^^^^^^^^^^^^

**File Size**

.. code-block:: python

    from Naked.toolshed.system import file_size

    size = file_size('test.txt')
    print(size) # prints size of 'test.txt' in current working directory in bytes

**File Modification Time and Date**

.. code-block:: python

    from Naked.toolshed.system import file_mod_time

    m_time = file_mod_time('test.txt')
    print(m_time) # prints 'Wed Jan 29 23:49:04 2014'


.. _file-listings-examples:

File Listings Examples
^^^^^^^^^^^^^^^^^^^^^^^^^

For the following examples, the test directory contains the files: 'test.txt', 'pytest.py', and 'rbtest.rb'

**All Files in Current Working Directory**

.. code-block:: python

    from Naked.toolshed.system import list_all_files_cwd

    file_list = list_all_files_cwd()
    for x in file_list:
        print(x)

    # prints:
    #   test.txt
    #   pytest.py
    #   rbtest.rb

**All Files in Target Directory**

.. code-block:: python

    from Naked.toolshed.system import list_all_files

    dir_path = make_path('path', 'to', 'test')
    file_list = list_all_files(dir_path)
    for x in file_list:
        print(x)

    # prints:
    #   test.txt
    #   pytest.py
    #   rbtest.rb

**Filter Files by File Extension in Current Working Directory**

.. code-block:: python

    from Naked.toolshed.system import list_filter_files_cwd

    file_list = list_filter_files_cwd('.py')
    for x in file_list:
        print(x)

    # prints:
    #   pytest.py

**Filter Files by Wildcard**

.. code-block:: python

    from Naked.toolshed.system import list_match_pattern

    file_list = list_match_pattern('./*.py')
    for x in file_list:
        print(x)

    # prints:
    #   pytest.py


.. _make-directory-examples:

Directory Write Examples
^^^^^^^^^^^^^^^^^^^^^^^^^

**Make Directory When it Does Not Exist**

.. code-block:: python

    from Naked.toolshed.system import make_dirs

    if make_dirs('test'):
        print('success') # prints 'success'
    else:
        print('fail')

**Make Directory When it Does Exist**

.. code-block:: python

    from Naked.toolshed.system import make_dirs

    if make_dirs('test'):
        print('success')
    else:
        print('fail') # prints 'fail'


.. _data-stream-examples:

Data Stream Examples
^^^^^^^^^^^^^^^^^^^^^^^

**Standard Output Stream Write, With Newline**

.. code-block:: python

    from Naked.toolshed.system import stdout

    stdout('This is a test string')

    # prints 'This is a test string\n' to standard output with OS dependent newline character(s)

**Standard Output Stream Write, Without Newline**

.. code-block:: python

    from Naked.toolshed.system import stdout_xnl

    stdout_xnl('This is a test string')

    # prints 'This is a test string' to standard output

**Standard Output Stream Write with Iterable Object, With Newline**

.. code-block:: python

    from Naked.toolshed.system import stdout_iter

    the_list = ['test', 'this', 'string']
    stdout_iter(the_list)

    # prints to standard output:
    #   test
    #   this
    #   string

**Standard Output Stream Write with Iterable Object, Without Newline**

.. code-block:: python

    from Naked.toolshed.system import stdout_iter_xnl

    the_list = ['1', ' ' , '2', ' ' , '3']
    stdout_iter_xnl(the_list)

    # prints '1 2 3' to standard output

**Standard Error Stream Write, With Newline, with Exit Status Code 1**

.. code-block:: python

    from Naked.toolshed.system import stderr

    stderr("Um, that was an error.", 1)

    # prints 'Um, that was an error.\n' to standard output with OS dependent newline character(s) and raises SystemExit(1)

**Standard Error Stream Write, Without Newline, Without SystemExit**

.. code-block:: python

    from Naked.toolshed.system import stderr_xnl

    stderr_xnl("Um, that was an error.")

    # prints 'Um, that was an error' to standard error and does not raise SystemExit()


.. _application-exit-examples:

Application Exit Examples
^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Exit with Zero Status Code**

.. code-block:: python

    from Naked.toolshed.system import exit_success

    # successful code here
    exit_success() # raises SystemExit(0)

**Exit with Status Code 1**

.. code-block:: python

    from Naked.toolshed.system import exit_failure

    # failing code here
    exit_failure() # raises SystemExit(1)

**Exit with Any Status Code**

.. code-block:: python

    from Naked.toolshed.system import exit_with_status

    # failing code here
    exit_with_status(10) # raises SystemExit(10)
