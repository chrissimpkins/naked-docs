The Naked Executable
======================

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

Usage
^^^^^^

.. code-block:: bash

	naked build

This will compile the C library files in the ```Naked.toolshed.c.<module>`` path.  See the library documentation for more information about the available Naked toolshed modules.

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
The *make* command builds the directory tree and files for a new Naked project.  You have the option to configure your project with a YAML file or via command line prompts.  The file and directory structure for command line parsing logic, command development, testing, profiling/benchmarking, licensing, application documentation, and deployment are included in the project.  Help, version, and usage commands are implemented for you in every new project. You simply write the corresponding text that is displayed to the user.

The goal is to allow you to click and begin coding your project without the tedious setup tasks that are common to all new projects.

naked.yaml Settings File Project Generation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The structure of the naked.yaml project settings file is:

.. code-block:: yaml

	application: <application-name>
	developer: <developer-name>
	license: <license-name>

Here is an example of the naked.yaml file from status:

.. code-block:: yaml

	application: status
	developer: Christopher Simpkins
	license: MIT License

Save this in the top level of your new project directory and then run the following command:

.. code-block:: bash

	naked make

Naked will detect the settings file, prompt you to confirm your settings, and then use this information to build the new project.  You will have the option to modify your project settings before the project writes to disk.

Command Line Prompt Project Generation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Use the following command syntax to initiate the command line prompts for a new Naked project:

.. code-block:: bash

	naked make <application-name>

Naked will then prompt you to enter the developer's or organization's name and the license type.

Where the Information is Used
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Your application name becomes the executable command that is used at the command line for your application and is also the top level of your Python module directory structure for imports in your project (and for use by others if you distribute a library).  The information is also used to generate your main application module, LICENSE file, README file, and settings.py file.

The Project License
^^^^^^^^^^^^^^^^^^^^
Naked parses your license type response and attempts to generate your project LICENSE file.  This is performed with a case-insensitive attempt to match one of the following strings at *the beginning* of your response:

* Apache
* BSD
* GPL
* LGPL
* MIT
* Mozilla

If your license type is identified, the entire text of the license is populated in your LICENSE file for you along with a copyright statement for the current year and

Make Command Help
^^^^^^^^^^^^^^^^^^

.. code-block:: bash

	naked make help


.. _test-command-label:

The Test Command
-----------------
The test command
