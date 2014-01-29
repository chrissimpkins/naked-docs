Install Guide
==============

.. note::

	If you have an installed version of Naked and want to upgrade it, see the :doc:`Upgrade Guide </upgrade>`.

Use one of the following methods to install your first version of Naked.

Install with pip
-----------------
To install Naked with `pip <http://www.pip-installer.org/>`_, use the following command:

.. code-block:: bash

	pip install Naked


Git Clone and Install
----------------------
Navigate to the directory where you would like to pull the Naked source and then use git to clone the Naked repository with the following command:

.. code-block:: bash

	git clone https://github.com/chrissimpkins/naked.git

Navigate to the top level of the source repository and run the following command:

.. code-block:: bash

	python setup.py install

The cloned repository can be safely deleted after the install.


Download and Install
---------------------
Download the `zip <https://github.com/chrissimpkins/naked/zipball/master>`_ or `tar.gz <https://github.com/chrissimpkins/naked/tarball/master>`_ source archive and decompress it locally. Navigate to the top level of the source directory and run the following command:

.. code-block:: bash

	python setup.py install

The downloaded source file archive can be safely deleted after the install.


Confirm Install
----------------
To confirm your install, type ``naked --version`` on the command line.  This will display the installed version of the Naked framework.
