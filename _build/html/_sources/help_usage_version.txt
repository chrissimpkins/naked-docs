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
The version text is a concatenated string that is made from the ``major_version``, ``minor_version``, and ``patch_version`` strings in the ``PROJECT/lib/PROJECT/settings.py`` file.  These should be set as Python strings by placing quotes around the numerals.

The ``settings.py`` version variables should look like the following:

.. code-block:: python

	#------------------------------------------------------------------------------
	# Version Number
	#------------------------------------------------------------------------------
	major_version = "0"
	minor_version = "1"
	patch_version = "0"

By default, the version text for an application named 'testapp' is displayed like this:

.. code-block:: bash

	$ testapp --version
	  testapp 0.1.0

As you increment your version numbers with new releases, the new version will be displayed when a user requests it.

.. note::

  	The version number settings in the settings.py file are imported into your setup.py file on new installs and releases to PyPI with the ``naked dist`` commands.  Make sure that they are correct for your release if you intend to use these features.

You can modify the displayed string format in this block of your app.py file:

.. code-block:: python

	    elif c.version():
	        from PROJECT.settings import app_name, major_version, minor_version, patch_version
	        # ** modify the string below to change the version text that is displayed to the user **
	        version_display_string = app_name + ' ' + major_version + '.' + minor_version + '.' + patch_version
	        print(version_display_string)
	        sys.exit(0)

For example, to remove the display of a patch version altogether, change the ``version_display_string`` assignment to:

.. code-block:: python

	version_display_string = app_name + ' ' + major_version + '.' + minor_version

.. _full version of file: https://github.com/chrissimpkins/naked/blob/master/lib/Naked/settings.py


How to Remove the Help, Version, & Usage Commands
---------------------------------------------------
These commands are completely optional and are implemented as a convenience.  The parsing logic and standard output writes are removed by either commenting out or deleting the following blocks of code in your ``app.py`` file:

.. code-block:: python

    if c.help():
        from {{app_name}}.settings import help as {{app_name}}_help
        print({{app_name}}_help)
        sys.exit(0)
    elif c.usage():
        from {{app_name}}.settings import usage as {{app_name}}_usage
        print({{app_name}}_usage)
        sys.exit(0)
    elif c.version():
        from {{app_name}}.settings import app_name, major_version, minor_version, patch_version
        version_display_string = app_name + ' ' + major_version + '.' + minor_version + '.' + patch_version
        print(version_display_string)
        sys.exit(0)

In your project, the ``{{app_name}}`` template strings are replaced with your application name.

.. warning::

	Since these code blocks are placed above your command logic, make sure that you change your first 'elif' to an 'if' statement if you have already started development below this level.
