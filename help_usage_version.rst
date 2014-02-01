Help, Usage, and Version Commands
===================================

Implementation of Commands in a Naked Project
----------------------------------------------

When you create a new Naked project with the ``naked make`` command, the command line parsing logic for help, usage, and version information requests is implemented for you.  This allows users to request this information from your application with any of the following:

Help
^^^^^^

.. code-block:: bash

	<executable> -h


.. code-block:: bash

	<executable> --help


.. code-block:: python

	<executable> help


Usage
^^^^^^

.. code-block:: bash

	<executable> --usage


.. code-block:: bash

	<executable> usage


Version
^^^^^^^^

.. code-block:: bash

	<executable> -v


.. code-block:: bash

	<executable> --version


.. code-block:: bash

	<executable> version


How to Set Your Help Text
----------------------------

The help text is assigned to the ``help`` variable in the ``PROJECT/lib/PROJECT/settings.py`` file.  Modify this string and save the file. It will be published to the standard output stream for users when they request application help with the above syntax.

Here is an example that includes the initial part of the ``naked`` executable help text (`full version of file`_):

.. code-block:: python

	help = """
	---------------------------------------------------
	 Naked
	 A Python command line application framework
	 Copyright 2014 Christopher Simpkins
	 MIT license
	---------------------------------------------------

	ABOUT

	The Naked framework includes the "naked" executable and the Python toolshed library.  The naked executable is a command line tool for application development, testing, profiling, and deployment.  The toolshed library contains numerous useful tools for application development that can be used through standard Python module imports.  These features are detailed in the documentation (link below).

	USAGE

	The naked executable syntax is:

	  naked <primary command> [secondary command] [option(s)] [argument(s)]

	# more...
	"""

Note the triple quote format that allows you to write multi-line strings in Python.


How to Set Your Usage Text
---------------------------
The usage text is assigned to the ``usage`` variable in the ``PROJECT/lib/PROJECT/settings.py`` file.  Modify this string and save the file.  It will be published to the standard output stream for users when they request application usage help with the above syntax.

Here is an example of the string from the ``naked`` executable (`full version of file`_):

.. code-block:: python

	usage = """
	Usage: naked <primary command> [secondary command] [option(s)] [argument(s)]
	--- Use 'naked help' for detailed help ---
	"""

How to Set Your Version Text
-----------------------------
The version text is a concatenated string that is made from the ``major_version``, ``minor_version``, and ``patch_version`` strings in the ``PROJECT/lib/PROJECT/settings.py`` file.  These should be set as Python strings by placing either double or single quotes around the numerals.

.. _full version of file: https://github.com/chrissimpkins/naked/blob/master/lib/Naked/settings.py
