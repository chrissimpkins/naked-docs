The Toolshed Library Overview
==============================

The toolshed library includes standard Python modules and C source files that can be compiled into binaries which Python will import with the typical syntax.  The C source code is compiled with the ``naked build`` command (`Build Command Documentation`_).

The library includes the following modules:

Benchmarking Module
--------------------

**Standard Module Import**: ``Naked.toolshed.benchmarking``

**C Module Import**: ``Naked.toolshed.c.benchmarking``

The benchmarking module includes decorators for timed testing of methods and functions over a series of 10 trials x 10 - 1 million repetitions. This includes a decorator that runs a standardized built-in Python method in sequence with your function or method for comparison.

Documentation: coming soon...


Casts Module
-------------

**Standard Module Import**: ``Naked.toolshed.casts``

**C Module Import**: ``Naked.toolshed.c.casts``

The casts module includes functions that cast built-in Python types to Naked type extensions.  This allows you to use the same type casting syntax that Python uses for the built-in types (e.g. the Python str() is xstr() for the Naked XString() type).

Documentation: coming soon...


File Module
------------

**Standard Module Import**: ``Naked.toolshed.file``

**C Module Import**: ``Naked.toolshed.c.file``

The file module includes FileWriter and FileReader classes that perform I/O, including simple UTF-8 encoded reads and writes.

Documentation: coming soon...


Ink Module
-----------

**Standard Module Import**: ``Naked.toolshed.ink``

**C Module Import**: ``Naked.toolshed.c.ink``

The ink module includes text template and renderer classes to perform flexible text templating with the replacement tag syntax of your choice.  A Python dictionary is used to map replacement strings to the replacement tags.

Documentation: coming soon...


Network Module
----------------

**Standard Module Import**: ``Naked.toolshed.network``

**C Module Import**: ``Naked.toolshed.c.network``

The network module includes the HTTP class for simple GET and POST requests with text or binary data.

Documentation: coming soon...


Python Module
--------------

**Standard Module Import**: ``Naked.toolshed.python``

**C Module Import**: ``Naked.toolshed.c.python``

The python module includes Python interpreter version testing functions.

Documentation: coming soon...


Shell Module
-------------

**Standard Module Import**: ``Naked.toolshed.shell``

**C Module Import**: ``Naked.toolshed.c.shell``

The shell module includes external system, Ruby, & Node.js subprocess execution methods and environent variable testing methods.

Documentation: coming soon...


State Module
-------------

**Standard Module Import**: ``Naked.toolshed.state``

**C Module Import**: ``Naked.toolshed.c.cstate``

The state (and cstate C module - note the change in the naming convention for this module) include the StateObject, an object that automatically generates operating system, user and working directory, Python interpreter, time, & date data on instantiation.

Documentation: coming soon...


System Module
--------------

**Standard Module Import**: ``Naked.toolshed.system``

**C Module Import**: ``Naked.toolshed.c.system``

The system module includes functions for file and directory paths, file and directory existence testing, file extension testing, file listings, file filters, file metadata, and decorators that automatically prepend filepaths to filename arguments in methods and functions. It also includes functions for simple printing to the standard output and standard error streams with exit code handling.

Documentation: coming soon...


Types Module
--------------

**Standard Module Import**: ``Naked.toolshed.types``

**C Module Import**: ``Naked.toolshed.c.types``

The types module includes extensions to built-in Python dictionary, list, set, frozenset, tuple, deque, and string classes.  It also includes a new type, the PriorityQueue.  These extensions permit assignment of attributes to both mutable and immutable Python types with dictionary key to attribute name mapping in the constructor.  Dictionary values are mapped to the attribute value.  New methods for use with these common Python types are also available.

Documentation: coming soon...

.. _Build Command Documentation: http://docs.naked-py.com/executable.html#build-command-label
