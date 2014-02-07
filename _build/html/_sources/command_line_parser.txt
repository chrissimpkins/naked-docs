Command Line Parser
====================

The Naked framework provides a command line parser that is intended to make the transition from a user command string to a Python object seamless and to make the generated Command object easy to use in your application logic.

How it Works
-------------

The command string is parsed into a series of positional and command line syntax specific arguments that are easily accessible through Command object attribute lookups or instance methods.  If that statement was as clear as mud, here is an example that walks you through access to the commands, options, and their arguments.

Say you are developing a command suite application that expects a user to control the application with a command syntax like the following::

	<executable> <primary command> [secondary command] [short option(s)] [long option(s)] [argument to option]


Let's take a look at how you retrieve the information from the user input.

How to Import the Command Line Parser
---------------------------------------
The parser is available in the ``Naked.commandline`` module and can be imported into your ``app.py`` file (app.py file information in :doc:`naked_project_structure`) with:

.. code-block:: python

	import sys
	import Naked.commandline

If you created your project with the ``naked make`` command, this import is added to the generated ``app.py`` file for you.


How to Instantiate a Command Object
-------------------------------------
Create an instance of the command line parser with:

.. code-block:: python

	c = Naked.commandline.Command(sys.argv[0], sys.argv[1:])

The class is instantiated with two arguments.  The name of your executable and the remainder of the command line string.  The Python sys module takes care of both of these arguments for you.

.. note::

	Import the Python sys module in your ``app.py`` file in order to pass the entire command line string to the Naked Command constructor (as shown above)

The Primary and Secondary Commands
-------------------------------------

The parser creates a new attribute from the first positional argument to the executable that is named ``cmd`` (for the primary command) and an attribute for the second positional argument that is named ``cmd2`` (for the secondary or sub-command).  Assuming that you call your Command object instance, 'c', as I demonstrated above, these commands are accessible with the following attribute lookups:

.. code-block:: python

	primary_command = c.cmd
	secondary_command = c.cmd2

And you can test for the presence of a specific command in the same fashion:

.. code-block:: python

	if c.cmd == "command1":
		# do something
	elif c.cmd == "command2":
		# do something else
	elif c.cmd == "command3":
		# do yet another thing

The secondary command can be inserted into the application logic for each primary command like so:

.. code-block:: python

	if c.cmd == "command1":
		if c.cmd2 == "sub_command1":
			# do command1 branch 1
		elif c.cmd2 == "sub_command2":
			# do command1 branch 2
		elif c.cmd2 == "sub_command3":
			# do command1 branch 3

Options
---------

For the purposes of this discussion, I am going to call an option that looks like this ``-s`` a short option, one that looks like this ``--long`` a long option, and one that has the following appearance ``--flag=argument`` a flag.

The parser identifies options by the presence of the first '-' symbol in the string.  You can test for the presence of these option forms with a Command object method.

For exclusive options:

.. code-block:: python

	if c.option('-s') or c.option('--something'):
		# the user indicated this option, handle it
	elif c.option('-e') or c.option('--else'):
	 	# the user indicated this option, handle it

For non-exclusive, independent options:

.. code-block:: python

	if c.option('-s') or c.option('--something'):
		# the user indicated this option, handle it
	if c.option('-e') or c.option('--else'):
	 	# the user indicated this option, handle it

For non-exclusive, dependent options:

.. code-block:: python

	if c.option('-s') or c.option('--something'):
		if c.option('-e') or c.option('--else'):
	 		# the user indicated both options, handle them

The presence of a flag (as you'll recall, an option that looks like this ``--flag=argument``) is tested for with the ``flag()`` method:

.. code-block:: python

	if c.flag('--flag'):
		argument = c.flag_arg('--flag') # more information below on arguments!


Test for the Existence of Short and Long Options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
To determine whether there were one or more options in the command that the user submitted, use either of the following tests that return a boolean:

**Method Approach**

.. code-block:: python

	if c.option_exists():
		# there is at least one short option, long option, or flag in command
	else:
		# there are no options

**Attribute Approach**

.. code-block:: python

	if c.options:
		# there is at least one short option, long option, or flag in command
	else:
		# there are no options


Test for the Existence of Flags
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Flags are a subset of options.  The above option tests will always return True if this test is True.

**Method Approach**

.. code-block:: python

	if c.flags_exists():
		# at least one flag was present in the command
	else:
		# no flags were present in the command

**Attribute Approach**

.. code-block:: python

	if c.flags:
		# at least one flag was present in the command
	else:
		# no flags were present in the command


Arguments to Options
---------------------
Arguments to the options are retrieved with the ``arg()`` method for short and long options, and with the ``flag_arg()`` method for flags.  These methods return a string that contains the n+1 positional argument relative to the option name that you enter as the method argument, or the string that immediately follows the '=' character for a flag. Here are examples:

For a short option:

.. code-block:: python

	# user enters '-l python' in the command
	arg_value = c.arg('-l')
	print(arg_value)  # prints 'python'


For a long option:

.. code-block:: python

	# user enters '--language python' in the command:
	arg_value = c.arg('--language')
	print(arg_value)  #prints 'python'

For a flag:

.. code-block:: python

	# user enters '--language=python' in the command:
	arg_value = c.flag_arg('--language')
	print(arg_value)  #prints python


Other Available Command Attributes
------------------------------------
There is overlap in the naming of the Command object attributes in order to provide a flexible scheme that (hopefully) addresses most command line application needs.  For instance, if you are developing an application that does not require primary or secondary commands, and instead takes up to one option after the executable::

	<executable> [option]

then you could use an approach like the following:

.. code-block:: python

	# Example: <executable> --test
	if c.options:
	    if c.arg0 == '--test':
			# do something
	else:
		# there are no options

or alternatively,

.. code-block:: python

	# Example: <executable> --test
	if c.options:
		if c.first == '--test':
			# do something
	else:
		# there are no options

Here is the list of all available Command object attributes

================    ==================================================================
**Attribute**       **Definition**
----------------    ------------------------------------------------------------------
obj.app      		executable path
obj.argv     		list of command arguments (excluding the executable)
obj.argc     		number of command line arguments (excluding the executable)
obj.arg0     		the first positional argument (excluding the executable)
obj.arg1     		the second positional argument (excluding the executable)
obj.arg2     		the third positional argument (excluding the executable)
obj.arg3            the fourth positional argument (excluding the executable)
obj.arg4            the fifth positional argument (excluding the executable)
obj.first           the first positional argument
obj.second          the second positional argument
obj.third           the third positional argument
obj.fourth          the fourth positional argument
obj.fifth           the fifth positional argument
obj.arglp    		the last positional argument
obj.last            the last positional argument
obj.arg_to_exec     the first argument to the executable = obj.arg0
obj.arg_to_cmd      the first argument to a primary command = obj.arg1
obj.cmd             the primary command = first positional argument
obj.cmd2            the secondary command = second positional argument
obj.options         boolean for presence of one or more options
obj.flags           boolean for presence of one or more flags

================    ==================================================================


The naked Executable Args Command
----------------------------------
The ``naked`` executable ``args`` command will help you design your command syntax logic with the Naked parser.  Just pass a complete command example as an argument and the ``args`` command will display every parsed attribute, the truth testing for options and flags, and the result of argument assignments to options and flags.

Here is an example of how it is used:

.. code-block:: bash

  naked args 'testapp save something --unicode -s --name=file.txt'

and the output looks like this::

	Application
	-----------
	c.app = testapp

	Argument List Length
	--------------------
	c.argc = 5

	Argument List Items
	-------------------
	c.argobj = ['save', 'something', '--unicode', '-s', '--name=file.txt']

	Arguments by Zero Indexed Start Position
	----------------------------------------
	c.arg0 = save
	c.arg1 = something
	c.arg2 = --unicode
	c.arg3 = -s
	c.arg4 = --name=file.txt

	Arguments by Named Position
	---------------------------
	c.first = save
	c.second = something
	c.third = --unicode
	c.fourth = -s
	c.fifth = --name=file.txt

	Last Positional Argument
	------------------------
	c.arglp = --name=file.txt
	c.last = --name=file.txt

	Primary & Secondary Commands
	----------------------------
	c.cmd = save
	c.cmd2 = something

	Option Exists Tests
	------------------
	c.option_exists() = True
	c.options = True

	Option Argument Assignment
	--------------------------
	c.arg("--unicode") = -s
	c.arg("-s") = --name=file.txt

	Flag Exists Tests
	----------------
	c.flag_exists() = True
	c.flags = True

	Flag Argument Assignment
	------------------------
	c.flag_arg("--name") = file.txt


Syntax Validation
--------------------
Two types of command syntax validation are available.


Validation of at Least One Argument
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
You can confirm that there is at least one argument (including options) passed to the executable with the following:

.. code-block:: python

	import sys
	from Naked.commandline import app_validates_args

	if not c.app_validates_args():
		# handle invalid syntax (e.g. print usage)
		sys.exit(1) # exit application with non-zero exit status

This test confirms that the argument list length is > 0 (i.e. obj.argc > 0) and returns a boolean value.

Validation of a Primary Command
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
You can also confirm that there is a primary command that is passed to the executable for command suite style applications.  Use a test like this:

.. code-block:: python

	import sys
	from Naked.commandline import command_suite_validates

	if not c.command_suite_validates():
		# handle invalid syntax (e.g. print usage)
		sys.exit(1) # exit application with non-zero exit status

A primary command is defined as any non-option string (i.e. a string that does not begin with a '-' character).  The method returns a boolean value for this test.



