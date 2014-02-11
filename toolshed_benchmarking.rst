Toolshed: ``benchmarking``
============================

.. py:module:: Naked.toolshed.benchmarking

Import Benchmarking Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.benchmarking


Import Benchmarking C Module
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: python

    import Naked.toolshed.c.benchmarking

The C module must be compiled before you import it.  See the `naked build <http://docs.naked-py.com/executable.html#the-build-command>`_ documentation for more information.

Description
^^^^^^^^^^^^
The benchmarking module provides decorators for timed method and function testing.  The ``timer`` decorators perform timed runs of a method or function over a specified number of repetitions.  The ``timer_trials_benchmark`` decorators perform multiple timed trials of a method or function (over a specified number of repetitions per trial) and run an arbitrary timed Python method as a benchmark in sequence with the function or method tests.

The Python method that is used as a benchmark is an append of 10 integers to a Python list:

.. code-block:: python

    for j in range(repetitions):
        for i in range(10):
            L.append(i)

This is run over the same number of repetitions that the test method or function is run.  Garbage collection is discontinued during all tests performed in this module.

The total duration of the timed run is displayed in the ``timer`` report.

The duration for each of the 10 trials, the mean duration across the 10 trials (with standard deviation if NumPy is installed), the duration per function or method run, the duration of the benchmark Python method, and a ratio of the duration of the test method or function to the benchmark Python method are displayed in the ``timer_trials_benchmark`` report.

The default :py:func:`timer` and :py:func:`timer_trials_benchmark` decorators perform 100,000 repetitions of the test method or function.  Other decorators are available for between 10 and 1 million repetitions.

Classes
^^^^^^^^

None

Decorators
^^^^^^^^^^^^

.. py:decorator:: timer

    100,000 repetitions of the decorated function or method

.. py:decorator:: timer_10

    10 repetitions of the decorated function or method

.. py:decorator:: timer_100

    100 repetitions of the decorated function or method

.. py:decorator:: timer_1k

    1,000 repetitions of the decorated function or method

.. py:decorator:: timer_10k

    10,000 repetitions of the decorated function or method

.. py:decorator:: timer_1m

    1 million repetitions of the decorated function or method

.. py:decorator:: timer_trials_benchmark

    10 trials x 100,000 repetitions of the decorated function or method; 100,000 repetitions of the standard Python function

.. py:decorator:: timer_trials_benchmark_10

    10 trials x 10 repetitions of the decorated function or method; 10 repetitions of the standard Python function

.. py:decorator:: timer_trials_benchmark_100

    10 trials x 100 repetitions of the decorated function or method; 100 repetitions of the standard Python function

.. py:decorator:: timer_trials_benchmark_1k

    10 trials x 1,000 repetitions of the decorated function or method; 1,000 repetitions of the standard Python function

.. py:decorator:: timer_trials_benchmark_10k

    10 trials x 10,000 repetitions of the decorated function or method; 10,000 repetitions of the standard Python function

.. py:decorator:: timer_trials_benchmark_1m

    10 trials x 1 million repetitions of the decorated function or method; 1 million repetitions of the standard Python function


Examples
^^^^^^^^^

**Timer Tests**

.. code-block:: python

    from Naked.toolshed.benchmarking import timer

    @timer
    def test_func():
        test_list = []
        for x in range(100):
            test_list.append(x)

Example Result:

.. code-block:: bash

    Starting 100000 repetitions of test_func()...
    100000 repetitions of test_func : 1.12108016014 sec

**Benchmark Timer Tests**

.. code-block:: python

    from Naked.toolshed.benchmarking import timer_trials_benchmark

    @timer_trials_benchmark
    def test_func():
        test_list = []
        for x in range(100):
            test_list.append(x)

Example Result:

.. code-block:: bash

    Starting timed trials of test_func()..........
    Trial 1:    1.12006998062
    Trial 2:    1.09371995926
    Trial 3:    1.09064292908
    Trial 4:    1.09283995628
    Trial 5:    1.09147787094
    Trial 6:    1.1042740345
    Trial 7:    1.10318899155
    Trial 8:    1.10284495354
    Trial 9:    1.10802388191
    Trial 10:   1.10440087318
    --------------------------------------------------
    Mean for 100000 repetitions: 1.10114834309 sec
    Standard Deviation: 0.00872229881241
    Mean per repetition: 1.10114834309e-05 sec
    Mean for 100000 of benchmark function:0.131036162376 sec
    Ratio: 8.4033927972





