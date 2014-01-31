Naked Project Structure
========================

A Naked Project
-----------------
A Naked project is generated with the ``naked make`` command.  Here is the structure of the project.

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
                 |      PROJECT---|
                 |                commands---(__init__.py)
                 |                |
                 |                app.py
                 |                |
                 |                settings.py
                 |
                 MANIFEST.in
                 |
                 README.md
                 |
                 setup.cfg
                 |
                 setup.py

Project Description
--------------------

docs Directory
^^^^^^^^^^^^^^^
This directory contains your LICENSE and README.rst files.  The ``naked`` executable will make an attempt to generate a complete license file for you if you use the ``naked make`` command.  See the `naked executable documentation`_ for details.

.. note::

    Your README.rst file is used to generate the long description of your project in the setup.py file. This becomes the description that is displayed on your PyPI application page if you push to the PyPI repository.  You can use reStructuredText in this document.

tests Directory
^^^^^^^^^^^^^^^^
This is an "empty" directory (it actually includes an ``__init__.py`` file) for your unit tests if you choose to include them.

.. note::

    The ``naked test`` command expects your unit tests and/or test runners to be in this directory in order to run the tests.

lib Directory
^^^^^^^^^^^^^^
This directory is designated as the site of your application source code in the setup.py file.  In order to establish your project name as the top level directory for Python imports, the project name is repeated as a sub-directory in the lib directory (with an associated ``__init__.py`` file).  This allows you to perform imports with the syntax: ``import <PROJECT>.commands.<COMMAND-MODULE>``, or if you develop a library for other users, imports can be performed with the syntax: ``from <PROJECT>.<directory>.<module> import <object>``.

The ``lib/PROJECT`` directory contains:

* **commands** directory : the location for your application command modules
* **app.py** : your main application script
* **settings.py** : a project settings script. This is also the location of your help, usage, and version strings if you use the commands that the ``naked`` executable generates for you with ``naked make`` (`Make Command Docs`_).

MANIFEST.in File
^^^^^^^^^^^^^^^^^
A distutils source distribution file include spec file (`MANIFEST documentation`_).

README.md File
^^^^^^^^^^^^^^^
This Markdown file is populated with the name of your project.  It is simply there in case you choose to use `GitHub`_ as a source repository and would like to display a message that differs from the one in your README.rst file (which ends up as your project description on PyPI).  It is safe to remove this file if you do not need it.

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
