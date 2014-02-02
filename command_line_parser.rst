Command Line Parser
====================

The Naked framework provides a command line parser that is intended to make the transition from a user command string to a Python object seamless, and to make that Command object as easy to use as possible.

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

If you created your project with the ``naked make`` command, this import is added to the generated ``app.py`` file.


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

The Naked command line parser creates a new attribute for the first argument to the executable that is named ``cmd`` (for the primary command).  It also creates an attribute that is named ``cmd2`` (for the secondary or sub-command).  Assuming that you call your Command object instance, 'c', as I demonstrated above, these commands are accessible with the following attribute lookups:

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

The Naked parser identifies options by the presence of the first '-' symbol in the string.  You can test for the presence of these option forms with a Command object method.

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

Arguments
-----------
Arguments to the options are retrieved with the ``arg()`` method for short and long options, and with the ``flag_arg()`` method for flags.  Here are examples:

## TODO : examples





