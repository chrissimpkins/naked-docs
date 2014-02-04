Naked Project Structure
========================

A Naked Project
-----------------
A Naked project is generated with the ``naked make`` command (`Make Command Docs`_).  Here is the structure of the project.

Directory Structure
^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

        PROJECT---|
              |
              docs---|
              |      LICENSE
              |      |
              |      README.rst
              |
              tests---(__init__.py)
              |
              |
              lib----|
              |      PROJECT-------|
              |      |             commands---(__init__.py)
              |      |             |
              |      profiler.py   app.py
              |                    |
              |                    settings.py
              |
              MANIFEST.in
              |
              README.md
              |
              setup.cfg
              |
              setup.py


Directories
------------

commands Directory
^^^^^^^^^^^^^^^^^^^
The commands directory is there to hold any command modules that you develop. You can import them into your main application script with:

.. code-block:: python

    import PROJECT.commands.MODULE

or

.. code-block:: python

    from PROJECT.commands.MODULE import OBJECT

docs Directory
^^^^^^^^^^^^^^^
This directory contains your LICENSE and README.rst files.  The ``naked`` executable will make an attempt to generate a complete license file for you if you use the ``naked make`` command.  See the `naked executable documentation`_ for details.

lib Directory
^^^^^^^^^^^^^^
This directory is the top level of your application source code and the site within which your setup.py file is instructed to search for your Python source files.  In order to establish your project name as the top level directory for Python imports, the project name is repeated as a sub-directory in the lib directory (with an associated ``__init__.py`` file).  This allows you to perform imports with the syntax::

    import <PROJECT>.commands.<COMMAND-MODULE>

or if you develop a library for other users, imports can be performed with the syntax::

    from <PROJECT>.<directory>.<module> import <object>

The ``lib/PROJECT`` directory contains:

* **commands** directory : the location for your application command modules (see above)
* **app.py** : your main application script (see below)
* **settings.py** : a project settings script (see below). This is also the location of your help, usage, and version strings if you use the commands that the ``naked`` executable generates for you with ``naked make`` (`Make Command Docs`_).

tests Directory
^^^^^^^^^^^^^^^^
This is an "empty" directory (it actually includes an ``__init__.py`` file) for your unit tests if you choose to include them.

.. note::

    The ``naked test`` command expects your unit tests and/or test runners to be in this directory in order to run the tests.


Files
------

app.py File
^^^^^^^^^^^^
The app.py file is the main application script and the start of your script execution.  Your application begins execution in the main() function in this module.  It is pre-populated with module imports, the Naked command line parser, the Naked StateObject, and the necessary code to implement help, usage, and version commands if you use the ``naked make`` command to create your project.

LICENSE File
^^^^^^^^^^^^^
The LICENSE file is generated in the docs directory and the text of the license is automatically if you use ``naked make`` with one of the supported open source licenses.  More details are available in the `naked executable documentation`_.

MANIFEST.in File
^^^^^^^^^^^^^^^^^
A distutils source distribution file include spec file (`MANIFEST documentation`_).

profiler.py File
^^^^^^^^^^^^^^^^^
The profiler.py file is a profiling runner script.  Insert the code that you would like to profile in the designated code block and run it with the Python interpreter ``python profiler.py``.  cProfile and pstats are implemented for you.

README.md File
^^^^^^^^^^^^^^^
This Markdown file is populated with the name of your project.  It is simply there in case you choose to use `GitHub`_ as a source repository and would like to display a message that differs from the one in your README.rst file (which ends up as your project description on PyPI).  It is safe to remove this file if you do not need it.

README.rst File
^^^^^^^^^^^^^^^^
The reStructuredText file README.rst is used as the long description of your project in the setup.py file.  This text gets pushed to PyPI as your project description on your PyPI project page.  You can use the reStructuredText syntax in this file for formatting on PyPI.

.. note::

    Your README.rst file is used to generate the long description of your project in the setup.py file. This becomes the description that is displayed on your PyPI application page if you push to the PyPI repository.  You can use reStructuredText in this document.

settings.py File
^^^^^^^^^^^^^^^^^
The settings.py file contains project-specific settings.  This includes the string variables for your help, usage, and version implementations if you use the default Naked project that is generated with ``naked make``.

setup.cfg File
^^^^^^^^^^^^^^^
A Python setup configuration file (`config documentation`_).

setup.py File
^^^^^^^^^^^^^^
A Python project distribution & install settings file.  ``naked make`` populates this file with your project name, developer/organization name, and license type. (`setup documentation`_)



.. _naked executable documentation: executable.html#the-project-license
.. _Make Command Docs: executable.html#the-make-command
.. _MANIFEST documentation: http://docs.python.org/2/distutils/sourcedist.html#manifest-template
.. _GitHub: https://github.com
.. _config documentation: http://docs.python.org/2/distutils/configfile.html
.. _setup documentation: http://docs.python.org/2/distutils/setupscript.html
