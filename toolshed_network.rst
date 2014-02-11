Toolshed: ``network``
========================

.. py:module:: Naked.toolshed.network


Import Network Module
^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.network


Import Network C Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.c.network

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The network module contains a HTTP class that supports GET and POST requests. This module is built with the fantastic Python `requests library <http://docs.python-requests.org/>`_.

Classes
^^^^^^^^

.. py:class:: HTTP(url [,request_timeout=10])

    The HTTP class is instantiated with a URL string and has a default request timeout of 10 seconds.  The protocol (``http://`` or ``https://``) must be included in the URL string.  If the protocol is not included, a ``requests.exceptions.MissingSchema`` exception will be raised that can be caught and handled in your code.  Include a second argument to the constructor with the time in seconds in order to change this request timeout duration.

    :param str url: the URL for the HTTP method request
    :param int request_timeout: the duration of the request method timeout in seconds (default=10 seconds)


    .. py:method:: get()

        Perform a GET request for text. This method returns the contents of the response as a string that is encoded with the ``HTTP.res.encoding`` encoding type.  The requests library attempts to determine this encoding according to the encoding header in the response.  Returns False on connection error (e.g. non-existent URL path).

    .. py:method:: get_bin()

        Perform a GET request for binary data. This method returns the contents of the response as a bytes string type. Returns False on connection error (e.g. non-existent URL path)

    .. py:method:: get_bin_write_file([filepath] [, suppress_output=False] [, overwrite_existing=False])

        Perform a GET request for binary data and write to disk. Returns True on successful file write. Returns False on unsuccessful writes, including on connection errors (e.g. non-existent URL path)

        :param str filepath: the output file path for the binary file write. If the filepath is not specified, the current working directory path is prepended to the filename in the URL.  This path is then used for the file write.
        :param boolean suppress_output: suppress standard output stream status updates during download (default=False)
        :param boolean overwrite_existing: overwrite an existing file at the same output filepath (default=False)

    .. py:method:: get_status_ok()

        Perform a GET request and return a boolean value for the statement, "the response status code is in the 200 range". The returned text data can be retrieved from the ``HTTP.res.text`` attribute and returned binary data can be retrieved from ``HTTP.res.content``.

    .. py:method:: get_txt_write_file([filepath] [, suppress_output=False] [, overwrite_existing=False])

        Perform a GET request for text and write a UTF-8 encoded text file to disk.  Returns True on successful file write.  Returns False on unsuccessful writes, including on connection errors (e.g. non-existent URL path)

        :param str filepath: the output file path for the text file write. If the filepath is not specified, the current working directory path is prepended to the filename in the URL.  This path is then used for the file write.
        :param boolean suppress_output: suppress standard output stream status updates during download (default=False)
        :param boolean overwrite_existing: overwrite an existing file at the same output filepath (default=False)

    .. py:method:: post()

        Perform a POST request for text.  This method returns the contents of the response as a string that is encoded according to the ``HTTP.res.encoding`` response type.  The requests library attempts to determine this encoding according to the encoding header in the response.  Returns False on connection errors (e.g. non-existent URL path).

    .. py:method:: post_bin()

        Perform a POST request for binary data.  This method returns the contents of the response as a bytes string type. Returns False on connection errors (e.g. non-existent URL path)

    .. py:method:: post_bin_write_file([filepath] [, suppress_output=False] [, overwrite_existing=False])

        Perform a POST request for binary data and write to disk. This method returns True on successful file write and returns False on unsuccesful write, including on connection errors (e.g. non-existent URL path)

        :param str filepath: the output file path for the binary file write. If the filepath is not specified, the current working directory path is prepended to the filename in the URL.  This path is then used for the file write.
        :param boolean suppress_output: suppress standard output stream status updates during download (default=False)
        :param boolean overwrite_existing: overwrite an existing file at the same output filepath (default=False)

    .. py:method:: post_txt_write_file([filepath] [, suppress_output=False] [, overwrite_existing=False])

        Perform a POST request for text data and write a UTF-8 encoded text file to disk.  This method returns True on successful file write and returns False on unsuccesful writes, including on connection errors (e.g. non-existent URL path)

        :param str filepath: the output file path for the text file write. If the filepath is not specified, the current working directory path is prepended to the filename in the URL.  This path is then used for the file write.
        :param boolean suppress_output: suppress standard output stream status updates during download (default=False)
        :param boolean overwrite_existing: overwrite an existing file at the same output filepath (default=False)

    .. py:method:: post_status_ok()

        Perform a POST request and return a boolean value for the statement, "the response status code is in the 200 range".  The returned text data can be retrieved from the ``HTTP.res.text`` attribute and returned binary data can be retrieved from ``HTTP.res.content``.

    .. py:method:: response()

        Return the response object following a HTTP GET or POST request.  This is the same object that defines the ``HTTP.res`` attribute following one of these request types.  See The Response Object section below for details about the response object attributes.



The Response Object
^^^^^^^^^^^^^^^^^^^^^
The response object ``HTTP.res`` is available after a successful GET or POST request for a response from a server.  The response object and its attributes are accessible either directly with dot syntax or as the return value from the :py:meth:`HTTP.response` method. The attributes of the response object include:

* ``content`` - bytes string of the returned data
* ``encoding`` - string encoding applied to the returned text in the text attribute
* ``headers`` - dictionary of the response headers
* ``status_code`` - integer response status code
* ``text`` - text string encoded with the encoding type defined in the encoding attribute



Examples
^^^^^^^^^^

**Instantiation of Default HTTP Object**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/status/200')

**Instantation of HTTP Object with Adjustment of Request Timeout**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/status/200', request_timeout=20)

**GET Request for Text**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('https://raw.github.com/chrissimpkins/naked/master/README.md')
    if http.get_status_ok():
        text = http.res.text
        # do something with the text

**GET Request for Text, Alternate Approach**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('https://raw.github.com/chrissimpkins/naked/master/README.md')
    resp = http.get()
    if resp:
        # do something with the `resp` text

**GET Request for Binary Data**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('https://github.com/chrissimpkins/naked/tarball/master')
    if http.get_status_ok():
        data = http.res.content
        # do something with the data

**GET Request for Binary Data, Alternate Approach**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('https://github.com/chrissimpkins/naked/tarball/master')
    resp = http.get_bin()
    if resp:
        # do something with the `resp` data


**POST Request for Text**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/post')
    if http.post_status_ok():
        text = http.res.text
        # do something with the text

**POST Request for Text, Alternate Approach**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/post')
    resp = http.post()
    if resp:
        # do something with the `resp` text

**POST Request for Binary Data**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/post')
    if http.post_status_ok():
        data = http.res.content
        # do something with the data

**POST Request for Binary Data, Alternate Approach**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/post')
    resp = http.post_bin()
    if resp:
        # do something with the `resp` data

**Write Text File from GET Request**

.. code-block:: python

    import os
    from Naked.toolshed.network import HTTP

    filepath = os.path.join('test', 'naked_README.md')
    http = HTTP('https://raw.github.com/chrissimpkins/naked/master/README.md')
    if http.get_txt_write_file(filepath):
        # file write was successful
    else:
        # file write was not successful

**Write Binary File from GET Request**

.. code-block:: python

    import os
    from Naked.toolshed.network import HTTP

    filepath = os.path.join('test', 'naked.tar.gz')
    http = HTTP('https://github.com/chrissimpkins/naked/tarball/master')
    if http.get_bin_write_file(filepath):
        # file write was successful
    else:
        # file write was not successful

**Write Text File from GET Request, Overwrite Existing File**

.. code-block:: python

    import os
    from Naked.toolshed.network import HTTP

    filepath = os.path.join('test', 'naked_README.md')
    http = HTTP('https://raw.github.com/chrissimpkins/naked/master/README.md')
    if http.get_txt_write_file(filepath, overwrite_existing=True):
        # file write was successful
    else:
        # file write was not successful

**Write Binary File from GET Request, Overwrite Existing File**

.. code-block:: python

    import os
    from Naked.toolshed.network import HTTP

    filepath = os.path.join('test', 'naked.tar.gz')
    http = HTTP('https://github.com/chrissimpkins/naked/tarball/master')
    if http.get_bin_write_file(filepath, overwrite_existing=True):
        # file write was successful
    else:
        # file write was not successful

**Response Headers**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/status/200')
    if http.get_status_ok():
        headers = http.res.headers


**Response Status Code, 200 Range**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/status/200')
    if http.get_status_ok():
        status = http.res.status_code

**Response Status Code, Non-200 Range**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/status/404')
    if http.get_status_ok():
        status = http.res.status_code
    else:
        fail_status = http.res.status_code

**Response Content-Type**

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP('http://httpbin.org/status/200')
    if http.get_status_ok():
        content_type = http.res.headers['content-type']




