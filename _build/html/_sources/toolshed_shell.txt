Toolshed: ``shell``
======================

.. py:module:: Naked.toolshed.shell

Import Shell Module
^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.shell


Import Shell C Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.c.shell

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The ``shell`` module includes functions for the execution of system executables and scripts, and the :py:class:`Environment` class for access to shell environment variables.

Functions for the Execution of System Commands
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: execute(command)

    The ``execute`` function runs a shell command as a new process with the Python method ``subprocess.call()``.  The standard output or standard error stream data are displayed in the terminal immediately and **are not** returned to the calling function/method, rather the success or failure of the command execution is returned.

    :param string command: the complete command that is to be executed by the shell
    :rtype: (boolean) Defined as True = zero exit status code, False = non-zero exit status code

.. py:function:: muterun(command)

    The ``muterun`` function runs a shell command as a new process with the Python method ``subprocess.check_output()``.  There is no display of data in the terminal from the standard output or standard error streams of the executed command.  Instead, the content of these streams is returned to the calling code as a generic ``NakedObject`` with the standard output stream data, standard error stream data, and exit code mapped to the attributes ``NakedObject.stdout``, ``NakedObject.stderr``, and ``NakedObject.exitcode``, respectively.  These can be accessed with standard Python dot syntax and handled in your own code.

    :param string command: the complete command that is to be executed by the shell
    :rtype: NakedObject

        .. py:attribute:: NakedObject.stdout

            (bytes string) The ``stdout`` attribute of the returned NakedObject contains the standard output stream data on success and an empty bytes string on failure of the executed command.

        .. py:attribute:: NakedObject.stderr

            (bytes string) The ``stderr`` attribute of the returned NakedObject contains the standard error stream data on failure and an empty bytes string on success of the executed command

        .. py:attribute:: NakedObject.exitcode

            (integer) The ``exitcode`` attribute of the returned NakedObject contains the exit status code that is returned from the executed command.  This can be used to test for the success or failure of the command.  See examples below.

.. py:function:: run(command, suppress_stdout=False, suppress_stderr=False, suppress_exit_status_call=True)

    The ``run`` function provides a flexible approach to the execution of a shell command.  As with the ``execute()`` and ``muterun()`` functions, a complete command string is provided as the first parameter to the function.  It differs from the other functions in that there are options to suppress prints of standard output and standard error streams prints to the terminal by the executed command, and to suppress the raise of a ``SystemExit`` on return of a non-zero exit status code from the executed command (or from the shell if the executable was absent).  You can use different permutations of these parameter settings to determine how much of the executable output is displayed to the user.  Furthermore, you can permit the executable to return a non-zero exit status code which will terminate execution of your Python script.

    :param string command: the complete command that is to be executed by the shell
    :param boolean suppress_stdout: *optional*, suppress print of standard output to the terminal (default = False)
    :param boolean suppress_stderr: *optional*, suppress print of standard error to the terminal (default = False)
    :param boolean suppress_exit_status_call: *optional*, suppress raise of SystemExit for non-zero exit status codes from the executed command (default = True). When set to True, your Python script is able to continue execution despite failure of the shell command.
    :rtype: (bytes string or boolean) returns string containing standard output stream data on command execution success (irrespective of ``suppress_stdout`` setting), False on non-zero exit status code returned by the shell command (irrespective of the ``suppress_stderr`` setting).  The ``suppress_<stream>`` settings only affect the diplay of these data streams in the user's terminal.

JavaScript (Node.js) Execution Functions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: execute_js(file_path, arguments="")

    The ``execute_js()`` function runs the :py:func:`execute` function on a Node.js script file.  Instead of passing the command to be executed as the first parameter, pass a Node.js script filepath as the first parameter and any additional command arguments as the second parameter (*optional*).  The executed command is concatenated from these strings with the following code:

    .. code-block:: python

        if len(arguments) > 0:
            js_command = 'node ' + file_path + " " + arguments
        else:
            js_command = 'node ' + file_path

    :param string file_path: the filepath to the Node.js script that is to be executed by the shell
    :param string arguments: *optional*, any additional arguments to be used with your command as demonstrated above.


.. py:function:: muterun_js(file_path, arguments="")

    The ``muterun_js()`` function runs the :py:func:`muterun` function on a Node.js script file.  Instead of passing the command to be executed as the first parameter, pass a Node.js script filepath as the first parameter and any additional command arguments as the second parameter (*optional*).  The executed command is concatenated from these strings as demonstrated in the :py:func:`execute_js` function description above.

    :param string file_path: the filepath to the Node.js script that is to be executed by the shell
    :param string arguments: *optional*, any additional arguments to be used with your command as demonstrated above.

.. py:function:: run_js(file_path, arguments="")

    The ``run_js()`` function runs the :py:func:`run` function on a Node.js script file.  Instead of passing the command to be executed as the first parameter, pass a Node.js script filepath as the first parameter and any additional command arguments as the second parameter (*optional*).  The executed command is concatenated from these strings as demonstrated in the :py:func:`execute_js` function description above.

    :param string file_path: the filepath to the Node.js script that is to be executed by the shell
    :param string arguments: *optional*, any additional arguments to be used with your command as demonstrated above.


Ruby Script Execution Functions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: execute_rb(file_path, arguments="")

    The ``execute_rb()`` function runs the :py:func:`execute` function on a Ruby script file.  Instead of passing the command to be executed as the first parameter, pass a Ruby script filepath as the first parameter and any additional command arguments as the second parameter (*optional*).  The executed command is concatenated from these strings with the following code:

    .. code-block:: python

        if len(arguments) > 0:
            rb_command = 'ruby ' + file_path + " " + arguments
        else:
            rb_command = 'ruby ' + file_path

    :param string file_path: the filepath to the Ruby script that is to be executed by the shell
    :param string arguments: *optional*, any additional arguments to be used with your command as demonstrated above.


.. py:function:: muterun_rb(file_path, arguments="")

    The ``muterun_js()`` function runs the :py:func:`muterun` function on a Ruby script file.  Instead of passing the command to be executed as the first parameter, pass a Ruby script filepath as the first parameter and any additional command arguments as the second parameter (*optional*).  The executed command is concatenated from these strings as demonstrated in the :py:func:`execute_rb` function description above.

    :param string file_path: the filepath to the Ruby script that is to be executed by the shell
    :param string arguments: *optional*, any additional arguments to be used with your command as demonstrated above.

.. py:function:: run_rb(file_path, arguments="")

    The ``run_rb()`` function runs the :py:func:`run` function on a Ruby script file.  Instead of passing the command to be executed as the first parameter, pass a Ruby script filepath as the first parameter and any additional command arguments as the second parameter (*optional*).  The executed command is concatenated from these strings as demonstrated in the :py:func:`execute_rb` function description above.

    :param string file_path: the filepath to the Ruby script that is to be executed by the shell
    :param string arguments: *optional*, any additional arguments to be used with your command as demonstrated above.


Shell Command Execution Function Examples
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**execute() Shell Command**

.. code-block:: python

    from Naked.toolshed.shell import execute

    success = execute('curl https://raw.github.com/chrissimpkins/naked/master/README.md')
    if success:
        # the command was successful
    else:
        # the command failed or the executable was not present)

**muterun() Shell Command**

.. code-block:: python

    from Naked.toolshed.shell import muterun

    response = muterun('curl https://raw.github.com/chrissimpkins/naked/master/README.md')
    if response.exitcode == 0:
        # the command was successful, handle the standard output
        standard_out = response.stdout
        print(standard_out)
    else:
        # the command failed or the executable was not present, handle the standard error
        standard_err = response.stderr
        exit_code = response.exitcode
        print('Exit Status ' + exit_code + ': ' + standard_err)

**run() Shell Command, Default**

.. code-block:: python

    from Naked.toolshed.shell import run

    success = run('curl https://raw.github.com/chrissimpkins/naked/master/README.md')
    if success:
        # the command was successful, automatically prints to standard output
    else:
        # the command failed or the executable was not present, automatically prints to standard error

**run() Shell Command, Suppress Standard Output and Standard Error**

.. code-block:: python

    from Naked.toolshed.shell import run

    success = run('curl https://raw.github.com/chrissimpkins/naked/master/README.md', suppress_stdout=True, suppress_stderr=True)
    if success:
        # the command was successful, success contains the data from standard output.
        # standard output is not printed to terminal
    else:
        # the command failed or the executable was not present, success contains False
        # standard error is not printed to terminal

**run() Shell Command, Permit SystemExit on Failure**

.. code-block:: python

    from Naked.toolshed.shell import run

    success = run('curl http://bogussite.io', suppress_exit_status_call=False)
    if success:
        # if the command was successful, this block is executed
    else:
        # this command fails (non-existent site), print to standard error and raise SystemExit with non-zero exit status code

**execute_rb() a Ruby Script**

.. code-block:: python

    from Naked.toolshed.shell import execute_rb

    success = execute_rb('testscript.rb')
    if success:
        # the script run was successful, the standard output was automatically printed to terminal
    else:
        # the script run failed, the standard error was automatically printed to terminal

**muterun_rb() a Ruby Script**

.. code-block:: python

    from Naked.toolshed.shell import muterun_rb

    response = muterun_rb('testscript.rb')
    if response.exitcode == 0:
        # the command was successful, handle the standard output
        standard_out = response.stdout
        print(standard_out)
    else:
        # the command failed or the executable was not present, handle the standard error
        standard_err = response.stderr
        exit_code = response.exitcode
        print('Exit Status ' + exit_code + ': ' + standard_err)

**run_rb() a Ruby Script**

.. code-block:: python

    from Naked.toolshed.shell import run_rb

    success = run_rb('testscript.rb')
    if success:
        # the script run was successful, standard output automatically printed to terminal by default
    else:
        # the script run failed, standard error automatically printed to terminal by default
        # does not raise SystemExit by default

**execute_js() a JavaScript (Node.js) Script**

.. code-block:: python

    from Naked.toolshed.shell import execute_js

    success = execute_js('testscript.js')
    if success:
        # the script run was successful, the standard output was automatically printed to terminal
    else:
        # the script run failed, the standard error was automatically printed to terminal

**muterun_js() a JavaScript (Node.js) Script**

.. code-block:: python

    from Naked.toolshed.shell import muterun_js

    response = muterun_js('testscript.js')
    if response.exitcode == 0:
        # the command was successful, handle the standard output
        standard_out = response.stdout
        print(standard_out)
    else:
        # the command failed or the executable was not present, handle the standard error
        standard_err = response.stderr
        exit_code = response.exitcode
        print('Exit Status ' + exit_code + ': ' + standard_err)

**run_js() a JavaScript (Node.js) Script**

.. code-block:: python

    from Naked.toolshed.shell import run_js

    success = run_js('testscript.js')
    if success:
        # the script run was successful, standard output automatically printed to terminal by default
    else:
        # the script run failed, standard error automatically printed to terminal by default
        # does not raise SystemExit by default


Environment Class
^^^^^^^^^^^^^^^^^^^^

.. py:class:: Environment()

    The ``Environment`` class contains methods that provide access to shell environment variables.

    .. py:method:: is_var(variable_name)

        Determine the existence of a shell environment variable.

        :param string variable_name: the name of the test environment variable

        :rtype: (*boolean*) Boolean value for existence of the environment variable


    .. py:method:: get_var(variable_name)

        Return the value of a shell environment variable

        :param string variable_name: the name of the environment variable

        :rtype: (*string*) Value of the environment variable

    .. py:method:: get_split_var_list(variable_name)

        Returns a list of the strings in a shell environment variable assignment list (e.g. PATH).

        :param string variable_name: the name of the environment variable

        :rtype: (*list*) returns a list of strings that are split by the OS dependent separator symbol or an empty list if the variable is not present



Environment Examples
^^^^^^^^^^^^^^^^^^^^^^

**Create a New Environment Instance**

.. code-block:: python

    from Naked.toolshed.shell import Environment

    env = Environment()

**Test for Environment Variable**

.. code-block:: python

    from Naked.toolshed.shell import Environment

    env = Environment()
    if (env.is_var('PATH')):
        # the shell environment variable exists
    else:
        # the shell environment variable does not exist

**Get Value of Environment Variable**

.. code-block:: python

    env = Environment()
    if (env.is_var('PATH')):
        path_string = env.get_var('PATH')
        print(path_string)

**Iterate Through List of Environment Variable Strings**

.. code-block:: python

    env = Environment()
    if (env.is_var('PATH')):
        for i in env.get_split_var_list('PATH'):
            print(i)
