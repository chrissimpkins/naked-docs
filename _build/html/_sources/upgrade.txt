Upgrade Guide
==============

Upgrade with pip
-----------------
To upgrade Naked with `pip <http://www.pip-installer.org/>`_, use the following command:

.. code-block:: bash

	pip install --upgrade Naked

This will pull the most recent version from PyPI and install it on your system.


Git Clone and Upgrade
----------------------
Navigate to the directory where you would like to pull the new version of the Naked source and then use git to clone the Naked repository with the following command:

.. code-block:: bash

	git clone https://github.com/chrissimpkins/naked.git

Navigate to the top level of the source repository and run the following command:

.. code-block:: bash

	python setup.py install

The cloned repository can be safely deleted after the upgrade.


Download and Upgrade
---------------------
Download the new version of the `zip <https://github.com/chrissimpkins/naked/zipball/master>`_ or `tar.gz <https://github.com/chrissimpkins/naked/tarball/master>`_ source archive and decompress it locally. Navigate to the top level of the source directory and run the following command:

.. code-block:: bash

	python setup.py install

The downloaded source file archive can be safely deleted after the upgrade.


Confirm Upgrade
----------------------
Type ``naked --version`` to confirm that you have the latest version of Naked.
