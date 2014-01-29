Naked Executable
==================

The naked executable is a command line tool for application development, testing, and deployment.

The primary commands include:

* :ref:`build-command-label`   - Compile Naked C library code
* :ref:`dist-command-label`    - Deployment to PyPI
* :ref:`locate-command-label`  - Locate important project files
* :ref:`make-command-label`    - Generate a new project
* :ref:`test-command-label`    - Project testing

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

.. code-block:: bash

	naked build help


.. _dist-command-label:

The Dist Command
-----------------
The dist command

.. _locate-command-label:

The Locate Command
-------------------
The locate command

.. _make-command-label:

The Make Command
-----------------
The *make* command builds the directory tree and project files for a new Naked project.  You have the option to configure your project with a YAML settings file ``naked.yaml`` or via command line prompts.

The file and directory structure for command line parsing logic, command development, testing, profiling/benchmarking, licensing, application documentation, and deployment are included in a new Naked project.  Help, version, and usage command handling is automatically implemented for you. Complete the strings that you intend to display to users (in the project ``settings.py`` file), and standard requests for help (e.g. ``<executable> --help``), usage (e.g. ``<executable> usage``), and version (e.g. ``<executable> --version``) will display the corresponding text.  For more information about these automatically generated commands, see :doc:`help_usage_version`.

The goal is to allow you to click and begin coding your project without the tedious setup tasks that are common to new projects.

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

.. code-block:: bash

	naked make help


.. _test-command-label:

The Test Command
-----------------
The test command
