Naked Executable
==================

The naked executable is a command line tool for application development, testing, profiling, and deployment. It is distributed with the Naked framework install.

The primary commands include:

* :ref:`args-command-label`    - View parsed command strings and truth tests
* :ref:`build-command-label`   - Compile Naked C library code
* :ref:`dist-command-label`    - Project deployment
* :ref:`locate-command-label`  - Locate important project files
* :ref:`make-command-label`    - Generate a new project
* :ref:`profile-command-label` - Project profiling
* :ref:`test-command-label`    - Project unit testing

.. _args-command-label:

The Args Command
-----------------
The ``args`` command will help you design your command syntax logic with the Naked parser.  Pass a complete command example as an argument to the command and it will display every parsed attribute, the truth testing for options and flags, and the result of argument assignments to options and flags.

Args Command Usage
^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

	naked args 'testapp save somestring --unicode -s --name=file.txt'

You can see an example of the output in the `Command Line Parser`_ documentation.

Args Command Help
^^^^^^^^^^^^^^^^^^^

.. code-block:: python

	naked args help


.. _build-command-label:

The Build Command
------------------
.. note::

	The build command requires an installed C compiler.  Naked does not install a compiler or confirm that one is installed on the user's system.

The Naked C toolshed library can be compiled from the C source code files with the *build* command.  Navigate to any level of your project directory and use the command:

Build Command Usage
^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

	naked build

This will compile the C library files in the ```Naked.toolshed.c.<module>`` path.  See the library documentation for more information about the available Naked toolshed modules.

Build Command Help
^^^^^^^^^^^^^^^^^^
Help is available with:

.. code-block:: python

	naked build help


.. _dist-command-label:

The Dist Command
-----------------
The dist command assists with distribution of your project to the `Python Package Index`_ (PyPI). This command can be used from any working directory in your Naked project.

The available secondary commands include:

all
^^^^
The ``all`` secondary command builds a source distribution, wheel distribution, and Windows installer distribution by running the distutils command ``python setup.py sdist bdist_wheel bdist_wininst upload``.  It is run with the following command:

.. code-block:: bash

	naked dist all

register
^^^^^^^^^
The ``register`` secondary command registers your Python project with PyPI.  This is a mandatory first step to distribute your project through PyPI and should be the first dist secondary command that you use for new project releases.  It is not necessary to run this again after the initial registration.

``register`` runs the distutils command ``python setup.py register`` and is run with:

.. code-block:: bash

	naked dist register

If you have not registered a project on PyPI from your local system before, you will receive prompts for your PyPI account information.

sdist
^^^^^^
The ``sdist`` secondary command prepares a source distribution for your current release and pushes it to PyPI.  This is performed by running the command ``python setup.py sdist upload`` and is run from the command line with:

.. code-block:: bash

	naked dist sdist

swheel
^^^^^^^^
The ``swheel`` secondary command prepares a source distribution and a wheel distribution for your current release and pushes it to PyPI.  This is performed by running the command ``python setup.py sdist bdist_wheel upload`` and is run from the command line with:

.. code-block:: bash

	naked dist swheel

wheel
^^^^^^
The ``wheel`` secondary command prepares a wheel distribution for your current release and pushes it to PyPI.  This is performed by running the command ``python setup.py bdist_wheel upload`` and is run from the command line with:

.. code-block:: bash

	naked dist wheel

win
^^^^
The ``win`` secondary command prepares a Windows installer for your current release and pushes it to PyPI.  This is performed by running the command ``python setup.py bdist_wininst upload`` and is run from the command line with:

.. code-block:: bash

	naked dist win

For more information about distutils and these release forms, please refer to the Python documentation.

Dist Command Help
^^^^^^^^^^^^^^^^^^^
Help is available for the dist command with:

.. code-block:: python

	naked dist help

.. _locate-command-label:

The Locate Command
-------------------
The locate command identifies several important file paths in your project.  I forget.  You forget.  It's simply there to help you remember.

The secondary commands are:

main
^^^^^
The main secondary command displays the file path to the project ``app.py`` file where you main application script is located.  You use the command like this:

.. code-block:: bash

	naked locate main

setup
^^^^^^
The setup secondary command displays the file path to the project ``setup.py`` file.

.. code-block:: bash

	naked locate setup

settings
^^^^^^^^^
The settings secondary command displays the file path to the project ``settings.py`` file. This is where your Naked project settings are located.

.. code-block:: bash

	naked locate settings

Locate Command Help
^^^^^^^^^^^^^^^^^^^^^
You can get help for the locate command with:

.. code-block:: python

	naked locate help

.. _make-command-label:

The Make Command
-----------------
The *make* command builds the directory tree and project files for a new Naked project.  You have the option to configure your project with a YAML settings file ``naked.yaml`` or via command line prompts.

The file and directory structure for command line parsing logic, command development, testing, profiling/benchmarking, licensing, application documentation, and deployment are included in a new Naked project.  Help, version, and usage command handling is automatically implemented for you. Complete the strings that you intend to display to users (in the project ``settings.py`` file), and standard requests for help (e.g. ``<executable> --help``), usage (e.g. ``<executable> usage``), and version (e.g. ``<executable> --version``) will display the corresponding text.  For more information about these automatically generated commands, see :doc:`help_usage_version`.

The goal is to allow you to click and begin coding your project without the tedious setup tasks that are common to many/most new projects.

naked.yaml Settings File Project Generation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The structure of a ``naked.yaml`` project settings file is:

.. code-block:: yaml

	application: <application-name>
	developer: <developer-name>
	license: <license-name>

Here is an example of the ``naked.yaml`` file for `status <https://pypi.python.org/pypi/status>`_:

.. code-block:: yaml

	application: status
	developer: Christopher Simpkins
	license: MIT License

Save your ``naked.yaml`` file in the top level of your new project directory and then run the following command in the same directory:

.. code-block:: bash

	naked make

Naked will detect the settings file, prompt you to confirm your settings, and then use this information to build the new project.  You will have the option to modify your project settings before the project writes to disk.

Command Line Prompt Project Generation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Use the following command syntax to initiate the command line prompts for a new Naked project:

.. code-block:: bash

	naked make <application-name>

Naked will then prompt you to enter the developer or organization name and the license type.

Where the Information is Used
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Your application name becomes the executable command that is used at the command line and is also the top level of your Python module directory structure for module imports.  The information is also used to generate your main application module, LICENSE file, README file, and settings.py file.

You can examine the project file templates in the `source repository`_ to see all of the string replacement sites.

The Project License
^^^^^^^^^^^^^^^^^^^^
Naked parses your license response and attempts to generate your project LICENSE file.  This is performed with a case-insensitive attempt to match one of the following strings at *the beginning* of your response:

* Apache
* BSD
* GPL
* LGPL
* MIT
* Mozilla

If your license type is identified, the entire text of the license is populated in your LICENSE file with the copyright statement, year, and the developer/organization name that you submitted.

For more information on the structure of a generated Naked project, see :doc:`naked_project_structure`.

Make Command Help
^^^^^^^^^^^^^^^^^^

.. code-block:: python

	naked make help


.. _profile-command-label:

The Profile Command
---------------------
The profile command runs cProfile and pstats on the code that you enter in test code block of your PROJECT/lib/profiler.py file.

Usage
^^^^^^^

.. code-block:: bash

	naked profile

The Profile
^^^^^^^^^^^^
The default profiler.py file sorts the pstats results with the 'time' argument.  You can modify this default in the profiler.py file.

Identification of the profiler.py File
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
naked performs a bottom up search over up to 6 directory levels from the working directory to identify the ``lib/profiler.py`` path.  Unless you have a deep project directory structure (and are in the bottom of one of these paths), this should allow you to run the command from any directory in your project.  It is not necessary for lib to be your working directory.

Profile Command Help
^^^^^^^^^^^^^^^^^^^^^^
Help is available for the profile command with:

.. code-block:: python

	naked profile help

.. _test-command-label:

The Test Command
-----------------
The test command allows you to run unit tests with the built-in Python unittest module (`v2`_, `v3`_), `nose`_, `pytest`_, or `tox`_.  The commands can be run from any directory level in your project (when the tests are located in your PROJECT/tests directory).

Usage
^^^^^^
.. code-block:: python

	naked test <secondary command> [argument]

The available secondary commands include:

nose
^^^^^
Runs nosetests on your PROJECT/tests directory

.. code-block:: python

	naked test nose

pytest
^^^^^^^
Runs py.test on your PROJECT/tests directory

.. code-block:: python

	naked test pytest

tox
^^^^
Runs tox on your PROJECT/tests directory.  This uses your tox.ini file settings by default.  To run a specific Python version, pass the **tox Python version argument** to the command (see examples below)

.. code-block:: python

	naked test tox        #runs tests with Python interpreter versions specified in tox.ini
	naked test tox py27   #runs tests with Python v2.7.x interpreter (must be installed)
	naked test tox py33   #runs tests with Python v3.3.x interpreter (must be installed)
	naked test tox pypy   #runs tests with pypy (installed version, must be installed)

unittest
^^^^^^^^^
Runs the built-in Python unittest module on the unit testing file that you specify as an argument to the command.  The file path argument is mandatory.  naked attempts to locate this test runner in your PROJECT/tests directory.

.. code-block:: python

	naked test unittest test_app.py

Identification of the tests Directory
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
A bottom up search is performed from the working directory over up to 6 directory levels to identify your tests directory.  If naked is not able to locate your tests directory, or if your files are in a different location, you will receive a failure message.

Test Command Help
^^^^^^^^^^^^^^^^^^
Help is available for the command with:

.. code-block:: python

	naked test help

.. _Python Package Index: http://pypi.python.org
.. _source repository: https://github.com/chrissimpkins/naked/tree/master/lib/Naked/templates
.. _v2: http://docs.python.org/2/library/unittest.html
.. _v3: http://docs.python.org/3/library/unittest.html
.. _nose: https://nose.readthedocs.org/en/latest/
.. _pytest: http://pytest.org/latest/
.. _tox: http://tox.readthedocs.org/en/latest/
.. _Command Line Parser: command_line_parser.html#the-naked-executable-args-command

