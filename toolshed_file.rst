Toolshed: ``file``
===================

.. py:module:: Naked.toolshed.file

Import File Module
^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.file


Import File C Module
^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.c.file

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The ``file`` module includes the :py:class:`FileReader` and :py:class:`FileWriter` classes.  These classes include a number of file I/O methods.

Classes
^^^^^^^^

.. py:class:: FileReader(file_path)

    The ``FileReader`` class is used for local file reads.  By default, the methods that deal with text return NFKD normalized UTF-8 encoded strings.  In Python 2, these are of the type ``unicode``, and in Python 3 they are of the type ``string``.  It is not necessary to close the file streams after you use these methods.

    :param string file_path: The path to the file.

    .. py:method:: read()

        Reads a text file with NFKD normalized UTF-8 string encoding.  Returns a unicode string in Python 2 and a string in Python 3.

        :returns: Python 3 ``string``, Python 2 ``unicode``

    .. py:method:: read_as(encoding)

        Reads a text file with a specified text encoding type.  Use a Python codecs encoding type as the method argument (``encoding``).

        :param string encoding: the Python codecs encoding type for the file text
        :returns: encoding specific Python string type
        :raises RuntimeError: if ``encoding`` is not specified

    .. py:method:: read_bin()

        Reads a binary file and returns a bytes string.

        :returns: bytes string

    .. py:method:: read_gzip([encoding])

        Reads a gzip compressed file and returns a bytes string. The ``encoding`` parameter is optional.  Include the parameter if the compressed file is Unicode text file and the method will attempt to decompress and read the file as a NFKD normalized UTF-8 encoded ``bytes`` string.

        :param string encoding: accepts an optional 'utf-8' string parameter if the compressed file is a UTF-8 encoded text file
        :returns: bytes string

    .. py:method:: readlines()

        Reads a text file by line with NFKD normalized UTF-8 encoding and returns a Python list containing each line of the file mapped to a list item.  In Python 2, the lines are of the type unicode and in Python 3 the lines are of the type string.

        :returns: Python list with each line in the file mapped to a list item.  List items are ``unicode`` in Python 2 and ``string`` in Python 3

    .. py:method:: readlines_as(encoding)

        Reads a text file by line with a specified text encoding type.  Returns a Python list containing each line of the file mapped to a list item.  Use a Python codecs encoding type as the method argument (``encoding``).  The list item types are dependent upon the encoding type that is passed as the parameter.

        :param string encoding: the Python codecs encoding type for the file text
        :returns: encoding specific Python string type


.. py:class:: FileWriter(file_path)

    The ``FileWriter`` class is used for local file writes.  It is not necessary to close the file streams after you use these methods.

    :param string file_path: The path to the file.

    .. py:method:: append(text)

        Append text to an existing text file at ``file_path``.  The existence of the file at ``file_path`` is confirmed before the write.  If it does not exist, an ``IOError`` is raised.  If the ``text`` string includes Unicode characters, the ``append`` method attempts to encode this as NFKD normalized UTF-8 text prior to the append.

        :param string text: The text to be appended to the existing file string.  Unicode encoded strings are acceptable.
        :raises IOError: if the file located at the ``file_path`` parameter does not exist.

    .. py:method:: gzip(data [, compression_level=6])

        Perform gzip compression of ``data`` with the zlib library and write to a file at ``file_path``.  The default compression level is 6 (integer range 0 - 9) in order to balance compression level and speed.   In most use cases, this approaches maximal compression with a significant reduction in the duration of time necessary to compress the data for the file write compared with the maximal compression setting.  Add a ``compression_level`` parameter to change this setting.

        :param string|bytes data: the string or bytes string to compress and write to the file at ``file_path``.
        :param integer compression_level: the integer value for the compression level.  Range is 0=none to 9=maximal.

        If the ``file_path`` string does not include it, ``.gz`` is added as the file extension to the ``file_path`` string.

    .. py:method:: safe_write(text)

        Write ``text`` to a text file at ``file_path`` if ``file_path`` does not already exist.  This method will not overwrite an existing file at the ``file_path``.  Use the :meth:`write` method to permit overwrites.  This method uses the system default encoding.  If the ``text`` string includes Unicode text, the method will attempt to write with NFKD normalized UTF-8 encoding.

        :param string text: The text to be written to the file at ``file_path``.
        :returns: boolean for file write.  ``True`` = new file write occurred; ``False`` = file exists and file write did not occur

    .. py:method:: safe_write_bin(data)

        Write ``data`` to a binary file at ``file_path`` if ``file_path`` does not already exist.  This method will not overwrite an existing file at ``file_path``.  Use the :meth:`write_bin` method to permit overwrites.

        :param bytes data: The data to be written to the file at ``file_path``.
        :returns: boolean for file write. ``True`` = new file write occurred; ``False`` = file exists and file write did not occur

    .. py:method:: write(text)

        Write ``text`` to a text file with the system default encoding. The ``write`` method will attempt to write with NFKD normalized UTF-8 encoding if the ``text`` string includes Unicode text.

        :param string text: The text to be written to the file at ``file_path``.

    .. py:method:: write_as(text, encoding)

        Write ``text`` to a text file with the specified ``encoding`` type.  Use a Python codecs encoding type as the second parameter to the method.

        :param string text: the text that is to be written to the file at ``file_path``.
        :param string encoding: the Python codecs string encoding type
        :raises RuntimeError: if ``encoding`` is not specified

    .. py:method:: write_bin(data)

        Write ``data`` to a binary file at ``file_path``.

        :param bytes data: The data to be written to the file at ``file_path``.


Examples
^^^^^^^^^^
**Create an Instance of a FileReader**

.. code-block:: python

    from Naked.toolshed.file import FileReader

    fr = FileReader('textdir/file.txt')


**Create an Instance of a FileWriter**

.. code-block:: python

    from Naked.toolshed.file import FileWriter

    fw = FileWriter('textdir/file.txt')


**File Read with ASCII Text**

.. code-block:: python

    from Naked.toolshed.file import FileReader

    fr = FileReader('textdir/file.txt')
    the_text = fr.read()

**File Write with ASCII Text**

.. code-block:: python

    from Naked.toolshed.file import FileWriter

    fw = FileWriter('textdir/file.txt')
    text = "A test string"
    fw.write(text)

**File Read with UTF-8 Encoded Unicode Text**

.. code-block:: python

    from Naked.toolshed.file import FileReader

    fr = FileReader('textdir/unicode.txt')
    u_txt = fr.read()

``u_txt`` is type ``unicode`` in Python 2 and type ``string`` in Python 3.

**File Write with UTF-8 Encoded Unicode Text, Python 2**

.. code-block:: python

    from Naked.toolshed.file import FileWriter

    fw = FileWriter('textdir/unicode.txt')
    u_txt = u'Here are some Tibetan characters ༄ དྷ'
    fw.write(u_txt)

**File Write with UTF-8 Encoded Unicode Text, Python 3**

.. code-block:: python

    from Naked.toolshed.file import FileWriter

    fw = FileWriter('textdir/unicode.txt')
    u_txt = 'Here are some Tibetan characters ༄ དྷ'
    fw.write(u_txt)

**File Append with ASCII Text**

.. code-block:: python

    from Naked.toolshed.file import FileWriter

    fw = FileWriter('textdir/existingfile.txt')
    text = 'And here is some more text for my file.'
    fw.append(text)

**File Append with UTF-8 Encoded Unicode Text, Python 2**

.. code-block:: python

    from Naked.toolshed.file import FileWriter

    fw = FileWriter('textdir/existingfile.txt')
    u_txt = u'Here are some Tibetan characters ༄ དྷ'
    fw.append(u_txt)

**File Append with UTF-8 Encoded Unicode Text, Python 3**

.. code-block:: python

    from Naked.toolshed.file import FileWriter

    fw = FileWriter('textdir/existingfile.txt')
    u_txt = 'Here are some Tibetan characters ༄ དྷ'
    fw.append(u_txt)

**Safe Write Text to a New File (Prevents File Overwrites)**

.. code-block:: python

    from Naked.toolshed.file import FileWriter

    fw = FileWriter('textdir/file.txt')
    text = 'And here is some more text for my file.'
    if fw.safe_write(text):
        # file write occurred
    else:
        # file exists and write did not occur

**File Read with Binary Data**

.. code-block:: python

    from Naked.toolshed.file import FileReader

    fr = FileReader('bindir/test.so')
    data = fr.read_bin()

**File Write with Binary Data**

.. code-block:: python

    from Naked.toolshed.file import FileWriter, FileReader

    fr = FileReader('bindir/test.so')
    fw = FileWriter('otherbindir/test2.so')
    data = fr.read_bin()
    fw.write_bin(data)

**Safe Write Binary Data to a New File (Prevents File Overwrites)**

.. code-block:: python

    from Naked.toolshed.file import FileWriter, FileReader

    fw = FileWriter('bindir/test.so')
    fr = FileReader('otherbindir/test2.so')
    data = fr.read_bin()
    if fw.safe_write_bin(data):
        # file write occurred
    else:
        # file exists and write did not occur

**gzip Compression and File Write**

.. code-block:: python

    from Naked.toolshed.file import FileWriter

    fw = FileWriter('bindir/index.html.gz')
    text = '<!DOCTYPE html><html lang="en"><body>Hi there, this is a test</body></html>'
    fw.gzip(text)

**Read gzip Compressed Data from File**

.. code-block:: python

    from Naked.toolshed.file import FileReader

    fr = FileReader('bindir/index.html.gz', encoding='utf-8')
    data = fr.read_gzip()


