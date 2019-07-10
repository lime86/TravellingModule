Software installation
=====================

Software packages for [YARR](https://gitlab.cern.ch/YARR/YARR) and
[BDAQ](https://gitlab.cern.ch/silab/bdaq53) are substantially different
with no common ground. Please follow the installation instructions for
each of the system separately, depending on the system at hand.

YARR-based system
-----------------

Use the [cleanup](https://gitlab.cern.ch/YARR/YARR/tree/cleanup) branch and follow the instructions on
[software installation](https://gitlab.cern.ch/YARR/YARR/tree/update_docs/docs/install.md) and [kernel driver installation](https://gitlab.cern.ch/YARR/YARR/tree/update_docs/docs/kernel_driver.md).

To enjoy supplementary plotting scripts, install ROOT6 on your CentOS7
PC `sudo yum install root`. The scripts have to be compiled
separately as shown
[here](https://gitlab.cern.ch/YARR/YARR/tree/update_docs/docs/rootscripts.md). Now when you
are back to this page, it is assumed that you managed to produce some
graphs from analog/digital scans and also familiarised yourself to some
degree with the
[scanConsole](https://gitlab.cern.ch/YARR/YARR/tree/update_docs/docs/scanconsole.md).


BDAQ-based system
-----------------

Use the dedicated [travelling_module](https://gitlab.cern.ch/silab/bdaq53/tree/travelling_module) branch
and follow instructions [here](https://gitlab.cern.ch/silab/bdaq53/tree/travelling_module#development).

Additional instructions: (to be updated)

Make sure you have a valid and clean Python 3.7 environment. The recommended method is to install [conda]( https://conda.io/miniconda.html).
Install dependencies using conda:
```bash
	# conda install numpy bitarray pyyaml scipy numba pytables matplotlib tqdm pyzmq blosc psutil coloredlogs
```
Go to a directory of your choice and clone the BDAQ53 repository using git:
```bash
	# git clone https://gitlab.cern.ch/silab/bdaq53.git
	# cd bdaq53
	# git checkout travelling_module
	# python setup.py develop
```
