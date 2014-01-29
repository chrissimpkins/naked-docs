
Naked
======

A Python Command Line Application Framework
--------------------------------------------

Naked (source: `PyPI`_, `GitHub`_) is a MIT licensed command line application framework that provides a range of features for Python application developers.

Examples include:

* **New Project Generator** : Create the directory structure and project file stubs with the naked executable:

.. code-block:: bash

    naked make

* **Simple Command to Python Object Parser** :

.. code-block:: python

    c = Naked.commandline.Command(sys.argv[0], sys.argv[1:])
    if c.cmd == 'hello' and c.cmd2 == "world":
        if c.option('--print'):
            print('Hello World!')

* **Simple Command Argument Management** :

.. code-block:: python

    if c.option_with_arg('-l') and c.option_with_arg('--framework'):
        language = c.arg('-l')               # user entered '-l Python'
        framework = c.arg('--framework')     # user entered '--framework Naked'
        print(framework + ' ' + language)   # prints 'Naked Python' to standard out

* **Simple Command Switch Management** :

.. code-block:: python

    if c.option('-s'):
        # do something
    elif c.option('-l'):
        # do something else

* **Simple State Management** :

.. code-block:: python

    if c.option('--string'):
        c.string = True
        c.number = False
    if c.option('--number'):
        c.string = False
        c.number = True

    # other stuff

    if c.string:
        # do this
    elif c.number:
        # do that

* **The Naked toolshed types library** includes extensions of commonly used Python types:

    * **XString** extends string
    * **XDict** extends dictionary
    * **XList** extends list
    * **XSet** extends set
    * **XFSet** extends frozenset
    * **XQueue** extends deque
    * **XPriorityQueue** adds a new type

* **The Ink Templating System** - a lightweight, flexible text templating system that allows you to define the replacement tag syntax.

* **The Naked StateObject** - a compendium of useful state information that is available with the instantation of a single object from any module. It includes data such as the Python interpreter version, operating system, date, time,

* **Faster compiled Naked C toolshed library** with an *optional* post-install compile

* **Every component of the framework is 100% optional**.  There is no project overhead if you don't want it.  You can build a new project and use ``argparse``, create your own project layout and use the Naked command line parser, or import one part of the library in a single module without the need to import it anywhere else in your project.  The goal is for Naked to help when you need it and get out of the way when you don't.  Naked + no long term commitment = win-win.



Contents
--------------

.. toctree::
   :maxdepth: 2

   index
   installation
   upgrade
   definitions
   quickstart
   naked_executable
   naked_project_structure

   ...

.. _PyPI: https://pypi.python.org/pypi?name=Naked&:action=display
.. _GitHub: https://github.com/chrissimpkins/naked

