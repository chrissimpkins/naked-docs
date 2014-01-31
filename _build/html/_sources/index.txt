
Naked
======

A Python Command Line Application Framework
--------------------------------------------

Naked (source: `PyPI`_, `GitHub`_) is a MIT licensed command line application framework that provides a variety of features for Python application developers.

Here is a sample:

New Projects
^^^^^^^^^^^^^

* **New Project Generator** : Create a complete project directory structure and project file stubs with the `naked executable`_:

.. code-block:: bash

    naked make

Command Line Parser
^^^^^^^^^^^^^^^^^^^^^

* **Simple Command to Python Object Parser** :

.. code-block:: python

    # positional strings in the command are command object attributes
    # short- (e.g. '-p') and long-form (e.g. '--print') options are tested with a method

    # user enters: <executable> hello world --print
    c = Naked.commandline.Command(sys.argv[0], sys.argv[1:])
    if c.cmd == 'hello' and c.cmd2 == "world":
        if c.option('--print'):
            print('Hello World!')

* **Simple Command Argument Management** :

.. code-block:: python

    # argument testing and assignment by command object methods

    # user enters: <executable> -l Python --framework Naked
    if c.option_with_arg('-l') and c.option_with_arg('--framework'):
        language = c.arg('-l')
        framework = c.arg('--framework')
        print(framework + ' ' + language)   # prints 'Naked Python' to standard out

* **Simple Command Switch Management** :

.. code-block:: python

    # switch testing by command object method

    if c.option('-s'):
        # do something
    elif c.option('-l'):
        # do something else

State Data
^^^^^^^^^^^^^

* **Simple State Management** :

.. code-block:: python

    # assign your own attributes to the command object for later use in your coding logic

    if c.option('--spam'):
        c.spam = True
        c.eggs = False
    if c.option('--eggs'):
        c.spam = False
        c.eggs = True

    # other stuff

    if c.spam:
        print("yum")
    elif c.eggs:
        print("yum"*2)

* **The StateObject** : a compendium of automatically generated user state information. It includes data such as the Python interpreter version, operating system, user directory path, current working directory, date, time, and more.

.. code-block:: python

    from Naked.toolshed.state import StateObject

    state = StateObject() # collects state information at time of instantiation

    working_directory = state.cwd
    if state.py2:
        print("In the directory " + working_directory + " and using the Python 2 interpreter")
    else:
        print("In the directory " + working_directory + " and using the Python 3 interpreter")


Networking
^^^^^^^^^^^
* GET and POST requests are as simple as:

.. code-block:: python

    from Naked.toolshed.network import HTTP

    http = HTTP("http://www.google.com")
    print(http.get())

    http = HTTP("http://httpbin.org/post")
    print(http.post())


File I/O
^^^^^^^^^
* Unicode (UTF-8) reads and writes:

.. code-block:: python

    from Naked.toolshed.file import FileReader, FileWriter

    r = FileReader('myfile.txt')
    u_txt = r.read_utf8()

    w = FileWriter('newfile.txt')
    w.write_utf8(u_txt)


Execution of System Applications and Scripts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **Simple System Subprocess Execution** : with non-zero exit code status handling & std err stream writes

.. code-block:: python

    from Naked.toolshed.shell import run

    print(run('curl http://www.naked-py.com'))

* **Simple Ruby Script Execution** : with non-zero exit code status handling & std err stream writes

.. code-block:: python

    from Naked.toolshed.shell import run_rb

    print(run_rb('ruby/testscript.rb'))

* **Simple Node.js Script Execution** : with non-zero exit code status handling & std err stream writes

.. code-block:: python

    from Naked.toolshed.shell import run_js

    print(run_js('node/testscript.js'))


Function, Method, Class Extensions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **The Naked toolshed types library** includes extensions of commonly used Python types:

    * **XString** extends the Python string
    * **XDict** extends the Python dictionary
    * **XList** extends the Python list
    * **XSet** extends the Python set
    * **XFSet** extends the Python frozenset
    * **XQueue** extends the Python deque
    * **XPriorityQueue** adds a new type

* **Faster, compiled C versions of the library modules** with an *optional* post-install compile for those who need the speed.


Text Templates
^^^^^^^^^^^^^^^

* **The Ink Templating System** - a lightweight, flexible text templating system that allows you to define the replacement tag syntax in your template documents. Available in the ``Naked.toolshed.ink`` library module.

Benchmarking
^^^^^^^^^^^^^^
* Benchmarking decorators are available for your methods and functions.  Insert a decorator above your function or method and get 10 trials of between 10 and 1 million repetitions of the code with comparison to a built-in test function. Comment it out and it's gone.

.. code-block:: python

    from Naked.toolshed.benchmarking import timer_trials_benchmark

    @timer_trials_benchmark
    def your_function(arg1, arg2):
        # your code

Profiling
^^^^^^^^^^
* The ``profiler.py`` script is added to every project in the path ``PROJECT/lib/profiler.py``. Insert your test code in the designated testing block and then run ``naked profile`` from any directory in your project.  cProfile and pstats profiling is implemented with default report settings (which you can modify in the ``profiler.py`` file if you'd like).

Flexible and No Commitment
^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **Every component of the framework is 100% optional**.  You determine how much (if any) of the Naked source you need in your project.  Building a project with the executable does not mandate use of the command parser, the automatically implemented help, usage, and version commands, or any part of the Naked toolshed library.

The goal is to help when you need it and get out of the way when you don't.

Contents
--------------

.. toctree::
   :maxdepth: 2

   installation
   upgrade
   definitions
   quickstart
   executable
   naked_project_structure
   help_usage_version
   change_log
   licenses

   ...

.. _PyPI: https://pypi.python.org/pypi?name=Naked&:action=display
.. _GitHub: https://github.com/chrissimpkins/naked
.. _naked executable: executable.html

