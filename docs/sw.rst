Software installation
=====================

Software packages for `YARR <https://gitlab.cern.ch/YARR/YARR>`__ and
`BDAQ <https://gitlab.cern.ch/silab/bdaq53>`__ are substantially
different with no common ground. Please follow the installation
instructions for each of the system separately, depending on the system
at hand.

YARR-based system
-----------------

Use the tagged version
`v1.0.0 <https://gitlab.cern.ch/YARR/YARR/tree/v1.0.0>`__ (master) and
follow the instructions on `software
installation <https://yarr.readthedocs.io/en/latest/install>`__ and
`kernel driver
installation <https://yarr.readthedocs.io/en/latest/kernel_driver>`__.

To enjoy supplementary plotting scripts, install ROOT6 on your CentOS7
PC ``sudo yum install root``. The scripts have to be compiled separately
as shown `here <https://yarr.readthedocs.io/en/latest/rootscripts>`__.
Now when you are back to this page, it is assumed that you managed to
produce some graphs from analog/digital scans and also familiarised
yourself to some degree with the
`scanConsole <https://yarr.readthedocs.io/en/latest/scanconsole>`__.

BDAQ-based system
-----------------

Use the dedicated
`travelling\_module <https://gitlab.cern.ch/silab/bdaq53/tree/travelling_module>`__
branch and follow instructions
`here <https://gitlab.cern.ch/silab/bdaq53/tree/travelling_module#development>`__.

Additional instructions: (to be updated)

Make sure you have a valid and clean Python 3.7 environment. The
recommended method is to install
`conda <https://conda.io/miniconda.html>`__. Install dependencies using
conda:

.. code:: bash

        $ conda install numpy bitarray pyyaml scipy numba pytables matplotlib tqdm pyzmq blosc psutil coloredlogs

Go to a directory of your choice and clone the BDAQ53 repository using
git:

.. code:: bash

        $ git clone https://gitlab.cern.ch/silab/bdaq53.git
        $ cd bdaq53
        $ git checkout travelling_module
        $ python setup.py develop
