QuickStart Guide
==================

Make Your Own Spam and Eggs
----------------------------
This guide will take you from an empty directory to a PyPI push of your first application release using features available in the Naked framework.  You will learn how to:

1. Create a new ``spameggs`` project with the ``naked make`` command
2. Implement the command line logic for your ``spameggs`` executable with the Naked parser
3. Import part of the Naked toolshed library for use in the application
4. Perform tox testing in multiple Python versions with the ``naked test`` command
5. Perform profiling with cProfile and pstatus using the ``naked profile`` command
6. Distribute your project to PyPI with the ``naked dist`` command.

Links are provided to other parts of the documentation where you can learn much more about the stages in this development process.

Make a New Project with ``naked make``
---------------------------------------
* Create a new directory and save a ``naked.yaml`` file in the directory that includes the following data:

.. code-block:: yaml

    application: spameggs
    developer: Guido
    license: MIT license

* Navigate to the directory in your terminal and run the command:

.. code-block:: bash

    naked make

* You will receive the following prompt:

.. code-block:: bash

    Detected a Naked project YAML setup file (naked.yaml).

    Please confirm the information below:

    ----------------------------------------------------------
     spameggs
     Copyright 2014 Guido
     MIT license
    ----------------------------------------------------------

    Is this correct? (y/n)

* Respond to the prompt with 'y'.

* naked displays the following information about your project structure:

.. code-block:: bash

    spameggs was successfully built.

    -----
    Main application script:  spameggs/lib/spameggs/app.py
    Settings file:  spameggs/lib/spameggs/settings.py
    Commands directory:  spameggs/lib/spameggs/commands
    setup.py file:  spameggs/setup.py
    -----

    Use 'python setup.py develop' from the top level of your project and you can begin testing your application with the executable, spameggs

* Let's follow the instructions in the last statement so that we can begin using the application from the command line. Enter the following in the top level directory that contains your setup.py file:

.. code-block:: bash

    python setup.py develop

Your application framework is all set for development. ``spameggs`` should be registered on your PATH so that you can use it.

Learn More
^^^^^^^^^^^
* `The Naked Executable <http://docs.naked-py.com/executable.html>`_
* `The Naked Make Command <http://docs.naked-py.com/executable.html#the-make-command>`_
* `The naked.yaml file <http://docs.naked-py.com/executable.html#naked-yaml-settings-file-project-generation>`_
* `How to create a project without a naked.yaml file <http://docs.naked-py.com/executable.html#command-line-prompt-project-generation>`_
* `How Naked creates your LICENSE file <http://docs.naked-py.com/executable.html#the-project-license>`_

Test Your Application Version Command
--------------------------------------
* Let's make sure that it is working.  ``naked make`` creates your version command for you.  Give it a try:

.. code-block:: bash

    $ spameggs --version
    spameggs 0.1.0

    $ spameggs -v
    spameggs 0.1.0

    $ spameggs version
    spameggs 0.1.0

* The displayed text automatically changes when you increment your version number in the ``spameggs/lib/spameggs/settings.py`` file and the format of the displayed string can be modified to your liking.  You can learn more with the links below.

Learn More
^^^^^^^^^^^
* `The help, usage, and version commands <http://docs.naked-py.com/help_usage_version.html>`_
* `How to set your version text <http://docs.naked-py.com/help_usage_version.html#how-to-set-your-version-text>`_
* `How to remove the Naked implementation of the version command <http://docs.naked-py.com/help_usage_version.html#how-to-remove-the-help-version-usage-commands>`_

Inspect Your Project Files
---------------------------
* Have a look through your project directory to familiarize yourself with what ``naked`` created for you.

Learn More
^^^^^^^^^^^
* `Diagram of the Naked Project Structure <http://docs.naked-py.com/naked_project_structure.html#directory-structure>`_
* `Directories that are created in a Naked Framework project <http://docs.naked-py.com/naked_project_structure.html#directories>`_
* `Files that are created in a Naked framework project <http://docs.naked-py.com/naked_project_structure.html#files>`_

Create Your Application
------------------------
``spameggs`` is going to perform the extremely important task of printing 'Spam and Eggs' to the standard output stream.  As with most academic exercises, this is going to be an extremely roundabout approach that is intended to be a demonstration of the capabilities of the framework rather than be the most efficient, or even correct (we are going to skip prints to std err and non-zero exit status returns for errors...), approach.

* Open your ``spameggs/lib/spameggs/app.py`` file in an editor and take a look through it.  ``main()`` is where execution of your application script begins.  ``naked`` included a few imports (the Python sys module, the Naked command line parser module, and the Naked state module for the StateObject).  It created an instance of the Naked parser (named ``c``) and also included the methods that handle help, usage, and version requests.  We tested the version commands above and we'll look at the help and usage below.  The last thing that ``naked`` inserts in this part of the file is a validation statement that confirms that the user entered a primary command (``c.command_suite_validates()``).

.. note::

    If you are not making a command suite application with syntax like this: ``<executable> <primary command> ...``, you can replace the ``command_suite_validates()`` method with the ``app_validates_args()`` method.  The latter confirms that at least one argument, including short options (e.g. ``-s``), long options (e.g. ``--long``), and flags (e.g. ``--flag=argument``), are included in the user's command.

* Let's add a command that has the following syntax:

.. code-block:: bash

    spameggs print [--meatsubstitute] <arg> [--overeasy] <arg>

* To do this, create a new module called ``seprinter`` in the path ``spameggs/lib/spameggs/commands`` with the following code:

.. code-block:: python

    #!/usr/bin/env python
    # encoding: utf-8
    # filename: seprinter.py

    from Naked.toolshed.ink import Template, Renderer

    class SpamPrinter:
        def __init__(self, the_meatsub, the_egg):
            self.meatsubstitute = the_meatsub
            self.egg = the_egg
            self.template_string = "{{spamtag}} and {{eggtag}}"

        def run(self):
            template = Template(self.template_string)
            r = Renderer(template, {'spamtag': self.meatsubstitute, 'eggtag': self.egg})
            spam_egg_string = r.render()
            print(spam_egg_string)


    if __name__ == '__main__':
        pass

An instance of the SpamPrinter class is created with ``the_meatsub`` and ``the_egg`` arguments and these are used to define instance properties that we subsequently use in the run() method.

Note how we imported the Naked toolshed library code for the Ink templating system in the command module code.  A Template instance is created from the template_string property on our SpamPrinter and it is rendered by passing a dictionary argument with keys that correspond to the strings inside your Template replacement tags.  The dictionary values are used to replace the corresponding tags in the template.  The opening ``{{`` and closing ``}}`` tags are the Ink template defaults.

Any component of the Naked toolshed library can be imported for use in your project with standard Python imports.  Use the path, ``Naked.toolshed.<MODULE>``, or for the compiled C versions of the library ``Naked.toolshed.c.<MODULE>`` (`requires the C source files to be compiled first! <http://docs.naked-py.com/executable.html#the-build-command>`_).

Learn More
^^^^^^^^^^^
* `The Naked toolshed library overview <http://docs.naked-py.com/toolshed_overview.html>`_
* The toolshed library documentation is in progress.  Hold tight! It is coming soon...

Handle Command Line Arguments for Your Application
----------------------------------------------------

* Now let's implement the command line argument handling.  Open the ``spameggs/lib/spameggs/app.py`` file in your editor and add the following to the PRIMARY COMMAND LOGIC code block:

.. code-block:: python

    elif c.cmd == 'print':
        if c.option('--meatsubstitute') and c.option('--overeasy'):
            from spameggs.commands.seprinter import SpamPrinter
            the_meat = c.arg('--meatsubstitute')
            the_eggs = c.arg('--overeasy')
            if state.py2:
                printer = SpamPrinter(the_meat, the_eggs)
            else:
                printer = SpamPrinter(the_meat.upper(), the_eggs.upper())
            printer.run()

        else:
            print("It would be extremely helpful if you enter '-- meatsubstitute Spam --overeasy Eggs' for the example.")

.. warning::

    Notice that we used 'elif' rather than if.  This logic is in sequence with the help, usage, and version tests that were included in your script above this level.  If you remove the Naked implementation of these commands and handle them yourself, make sure that you switch your first statement in the command tests to an 'if' statement.

Note how the Naked parser handles user entered arguments on the command line.  The primary command becomes an attribute of the ``c`` Command object that was instantiated earlier in the script.  ``cmd`` is the first positional argument to the executable (i.e. the primary command). See the link in the Learn More section below to view all of the available argument attributes and to learn how to use ``naked args`` to help plan your command logic tests with the Naked parser.

We begin by testing that the user entered the primary command 'print' (i.e. ``spameggs print ...``) .  If it was submitted, then we test for the presence of both of the options that are required to prepare our string.  The ``option()`` method returns a boolean for the question, "is the option argument that is passed to this method present?".  If these tests return True, the SpamPrinter object that we just developed is imported from the commands directory.  The arguments to these options that the user listed on the command line are retrieved with the ``arg()`` method of the Command object.  In this case, we assign them to local variables for clarity.

Next, we meet another branch in the logic that demonstrates one of the features of the Naked toolshed library StateObject (the instance is named 'state') that was automatically generated by ``naked`` when the project was built. This object collects a number of user state attributes at instantiation, including the version of the Python interpreter that they are using which we test for in the ``if state.py2:`` statement.  For Python 2 interpreters, we print the arguments to the ``meatsubstitute`` and ``overeasy`` options as is, and for Python 3 interpreters, we print them in all caps (with the ``string.upper()`` function).

Lastly, our run() method is called which executes the template replacements and prints the string to the standard output stream.

Let's give it a shot.  Try the following from your command line:

.. code-block:: bash

    spameggs print --meatsubstitute Spam --overeasy Eggs

If you are using Python 2.x, you should see ``Spam and Eggs`` in your terminal and if you are using Python 3.x, you should see ``SPAM and EGGS``.

The following areas of the documentation are helpful if you would like to delve into more detailed treatment of the parser.

Learn More
^^^^^^^^^^^
* `How the Command Parser Works <http://docs.naked-py.com/command_line_parser.html#how-it-works>`_
* `How to Import the Command Parser <http://docs.naked-py.com/command_line_parser.html#how-to-import-the-command-line-parser>`_
* `How to Instantiate a Command Object <http://docs.naked-py.com/command_line_parser.html#how-to-instantiate-a-command-object>`_
* `How to Handle Primary and Secondary Commands <http://docs.naked-py.com/command_line_parser.html#the-primary-and-secondary-commands>`_
* `How to Handle Options <http://docs.naked-py.com/command_line_parser.html#options>`_
* `How to Retrieve the Values for Arguments to Options <http://docs.naked-py.com/command_line_parser.html#arguments-to-options>`_
* `The List of All Command Object Attributes <http://docs.naked-py.com/command_line_parser.html#other-available-command-attributes>`_
* `Get Help with Your Command Parsing Logic Using the naked args Command <http://docs.naked-py.com/command_line_parser.html#the-naked-executable-args-command>`_


Create Your Help Text
------------------------
Now that we have an application, let's help our users out by providing some documentation when they request it with either ``spameggs --help``, ``spameggs -h``, or ``spameggs help``.  There is no need to add anything to the app.py file in order to handle these requests.  The ``naked make`` build takes care of that for you.

Open your ``spameggs/lib/spameggs/settings.py`` file in an editor and locate the help variable.  Add your help text like this:

.. code-block:: python

    help = """
    --------------------------
    spameggs
    Copyright 2014 Guido
    MIT license
    --------------------------

    ABOUT
      spameggs is a Python application that tells you about spam.  And it tells you about eggs.  Pipe it to whatever application might find that to be useful.

    USAGE
      spameggs [print] [--meatsubstitute] <arg> [--overeasy] <arg>

    OPTIONS
       --meatsubstitute      Takes a delectable meat substitute as an argument
       --overeasy            Takes an avian object as an argument
    """

and then give it a try:

.. code-block:: bash

    spameggs --help

Learn More
^^^^^^^^^^^
* `The help, usage, and version commands <http://docs.naked-py.com/help_usage_version.html>`_
* `How to Set Your Help Text <http://docs.naked-py.com/help_usage_version.html#how-to-set-your-help-text>`_
* `How to Remove the Help Command Created by naked make <http://docs.naked-py.com/help_usage_version.html#how-to-remove-the-help-version-usage-commands>`_


Create Your Usage Text
------------------------
To set your usage text, locate the usage variable in the ``spameggs/lib/spameggs/settings.py`` file that we just used above.  Let's add the usage string that we just used in the help text:

.. code-block:: python

    usage = """
    Usage: spameggs [print] [--meatsubstitute] <arg> [--overeasy] <arg>
    """

Then confirm that it works with:

.. code-block:: bash

    spameggs --usage

Learn More
^^^^^^^^^^^
* `The help, usage, and version commands <http://docs.naked-py.com/help_usage_version.html>`_
* `How to Set Your Usage Text <http://docs.naked-py.com/help_usage_version.html#how-to-set-your-usage-text>`_
* `How to Remove the Usage Command Created by naked make <http://docs.naked-py.com/help_usage_version.html#how-to-remove-the-help-version-usage-commands>`_


Testing with ``naked test``
-----------------------------
Time to unit test.  Let's set up a tox.ini file to test this in multiple versions of Python with the nose unit test runner.  If you are following along, both of these applications need to be installed in order to run the tests.  You can install them with pip:

.. code-block:: bash

    $ pip install tox
    $ pip install nose

In the top directory of your project (where your setup.py file is located), save the following in a file named ``tox.ini``:

.. code-block:: bash

    [tox]
    envlist = py27,py33
    [testenv]
    deps=nose
    commands=nosetests \
             "--where=tests"

This instructs tox to run the unit tests in our ``tests`` directory using the ``nosetests`` executable with our installed Python 2.7.x and Python 3.3.x versions (*Note*: both versions need to be installed locally to run these tests).  Refer to the tox documentation for instructions on how to test with other Python versions (including pypy).

Next, create a unit test file named ``test_spameggs.py`` in the tests directory:

.. code-block:: python

    #!/usr/bin/env python
    # coding=utf-8
    # file: test_spameggs.py

    import unittest
    from spameggs.commands.seprinter import SpamPrinter

    class SpamEggsTest(unittest.TestCase):

        def setUp(self):
            self.test_string = "{{spamtag}} and {{eggtag}}"
            self.template_string = SpamPrinter('Spam', 'Eggs').template_string

        def spam_eggs_test(self):
            """A test of spam, and of eggs"""
            self.assertEqual(self.test_string, self.template_string)

This test confirms that the template string is what we expect it to be and serves as a simple example.  From any directory in your project, run the following:

.. code-block:: bash

    naked test tox

This will launch tox and run the tests in Python 2.7 and 3.3 according to your specifications in the tox.ini file.  Confirm that they both pass and then we'll move on.

Learn More
^^^^^^^^^^^
`The Naked Test Command <http://docs.naked-py.com/executable.html#the-test-command>`_

Profiling with ``naked profile``
---------------------------------
Open the ``spameggs/lib/profiler.py`` file in your editor.  The file is stubbed with all of the source that you need to profile with cProfile and pstats.  The setup and profiled code blocks are indicated in the file.  You can enter the code that you intend to profile in the block below the ``pr.enable()`` statement:

.. code-block:: python

    #!/usr/bin/env python
    # encoding: utf-8

    import cProfile, pstats, StringIO

    def profile():
        #------------------------------------------------------------------------------
        # Setup a profile
        #------------------------------------------------------------------------------
        pr = cProfile.Profile()
        #------------------------------------------------------------------------------
        # Enter setup code below
        #------------------------------------------------------------------------------
        from spameggs.commands.seprinter import SpamPrinter


        #------------------------------------------------------------------------------
        # Start profiler
        #------------------------------------------------------------------------------
        pr.enable()

        #------------------------------------------------------------------------------
        # BEGIN profiled code block
        #------------------------------------------------------------------------------
        for x in range(10000):
            sp = SpamPrinter('Spam', 'Eggs')
            sp.run()


        #------------------------------------------------------------------------------
        # END profiled code block
        #------------------------------------------------------------------------------
        pr.disable()
        s = StringIO.StringIO()
        sortby = 'cumulative'
        ps = pstats.Stats(pr, stream=s).sort_stats(sortby)
        ps.strip_dirs().sort_stats("time").print_stats()
        print(s.getvalue())

    if __name__ == '__main__':
        profile()

Then use the following command from any directory in your project:

.. code-block:: bash

    naked profile

Naked will run the profiler.py file script and your report will be displayed in the terminal.

Learn More
^^^^^^^^^^^^
`The Profiler Command <http://docs.naked-py.com/executable.html#the-profile-command>`_

Distribution to PyPI with ``naked dist``
-----------------------------------------

.. warning::

    The following set of instructions are intended to demonstrate how you would distribute this application to PyPI.  If you run them, be aware that you will actually push spameggs to PyPI.  While this will instantly improve your reputation in the Python community, it is likely not what you intend to do.


Complete Your setup.py File
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
For an application that you really intend to release, you will need to fill in the remainder of the fields in your ``setup.py`` file before you perform the next steps.  Refer to the Python documentation for more information.

If you use the Naked toolshed library in your projects (including the command line parser), Naked should be listed as a dependency in your setup.py file with a line like this:

.. code-block:: python

    install_requires=['Naked'],

Register
^^^^^^^^^
To register your application on PyPI enter the following:

.. code-block:: bash

    naked dist register

If you have not previously registered an account on PyPI, use the prompts to do so now.  Otherwise, enter your account details.  When this command completes, your application will be registered.

Push to PyPI
^^^^^^^^^^^^^
You can push versions of your application to PyPI with the ``naked dist`` command as well.  There are secondary commands for various distribution types.  Let's push both a Python wheel and source distribution:

.. code-block:: bash

    naked dist swheel

See the ``dist`` command documentation link below for more information about the available release types.  When the command completes, your release will be live in the remote PyPI repository and ready to be installed by the masses.

Learn More
^^^^^^^^^^^
* `The Dist Command <http://docs.naked-py.com/executable.html#the-dist-command>`_
* `The Classify Command <http://docs.naked-py.com/executable.html#the-classify-command>`_


There you have it.  You started with an empty directory and ended with a push of your release to PyPI. Now go create something great.

