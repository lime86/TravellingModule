Software installation
=====================

Software packages for [YARR](https://gitlab.cern.ch/YARR/YARR) and
[BDAQ](https://gitlab.cern.ch/silab/bdaq53) are substantially different
with no common ground. Please follow the installation instructions for
each of the system separately, depending on the system at hand.

YARR-based system
-----------------

Use the tagged version [v1.1.0](https://gitlab.cern.ch/YARR/YARR/tree/v1.1.0) (master) and follow the instructions on
[software installation](https://yarr.web.cern.ch/yarr/install) and [kernel driver installation](https://yarr.web.cern.ch/yarr/kernel_driver).

To enjoy supplementary plotting scripts, install ROOT6 on your CentOS7
PC `sudo yum install root`. The scripts have to be compiled
separately as shown
[here](https://yarr.web.cern.ch/yarr/plotting). Now when you
are back to this page, it is assumed that you managed to produce some
graphs from analog/digital scans and also familiarised yourself to some
degree with the
[scanConsole](https://yarr.web.cern.ch/yarr/scanconsole).


BDAQ-based system
-----------------

Use the dedicated [travelling_module](https://gitlab.cern.ch/silab/bdaq53/tree/travelling_module) branch
and follow instructions [here](https://gitlab.cern.ch/silab/bdaq53/tree/travelling_module#development).

Additional instructions: (to be updated)

Make sure you have a valid and clean Python 3.7 environment. The recommended method is to install [conda]( https://conda.io/miniconda.html).
Install dependencies using conda:
```bash
	$ conda install numpy bitarray pyyaml scipy numba pytables matplotlib tqdm pyzmq blosc psutil coloredlogs
```
Go to a directory of your choice and clone the BDAQ53 repository using git:
```bash
	$ git clone https://gitlab.cern.ch/silab/bdaq53.git
	$ cd bdaq53
	$ git checkout travelling_module
	$ python setup.py develop
```
