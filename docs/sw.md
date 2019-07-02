Software installation
=====================

Software packages for [YARR](https://gitlab.cern.ch/YARR/YARR) and
[BDAQ](https://gitlab.cern.ch/silab/bdaq53) are substantially different
with no common ground. Please follow the installation instructions for
each of the system separately, depending on the system at hand.

YARR-based system
-----------------

YARR system has a dedicated portal
[readthedocs](https://yarr.readthedocs.io/en/devel). Please follow the
installations instructions there. For installation from scratch
generally, these steps are needed to be accomplished:

-   Clone and compile YARR software package from the [gitlab
    repository](https://gitlab.cern.ch/YARR/YARR)
-   Install custom PCIe kernel drivers
-   Follow hardware guidance for the type of DAQ card in your possession
-   Run basics scans such as digital, analog and threshold
-   Review acquired results

To enjoy supplementary plotting scripts, install ROOT6 on your CentOS7
PC `sudo yum install root`. The scripts have to be compiled
separately as shown
[here](https://yarr.readthedocs.io/en/devel/rootscripts/). Now when you
are back to this page, it is assumed that you managed to produce some
graphs from analog/digital scans and also familiarised yourself to some
degree with the
[scanConsole](https://yarr.readthedocs.io/en/devel/scanconsole/).

Local database (only available with YARR and Centos 7 at the moment)
--------------------------------------------------------------------

Local database as a concept is introduced to get the users some
experience of using databases. Eventually, all the results produced will
be uploaded to the production database. In the due course of the
production database being worked on, the local database will be used.
For the YARR DAQ system, a fork was created
[here](https://github.com/jlab-hep/Yarr). It includes the latest YARR
software and integrated local database. Please follow the detailed
installation instructions in the [wiki
page](https://github.com/jlab-hep/Yarr/wiki). Mind that eventually this
will be merged into the development and master branches of YARR
software.

This is how the local database and its installation works in general.
[MongoDB](https://www.mongodb.com/) classified as a NoSQL database
program, uses JSON-like documents with schema. It offers the simplicity
of development for databases with a none-straightforward structuring.
More data, files, structures and fields can be added as development
progresses giving flexibility this project needs at this stage of
development. This is very hard to achieve with an SQL database.

Several installation steps are needed, all detailed in the documentation
[here](https://github.com/jlab-hep/Yarr/wiki). A breakdown is below:

-   Installation of MongoDB dependencies
-   Installation of MongoDB
-   Installation of database backend
-   Installation of database viewer (front end)
-   Creation of the RD53A local database.
-   Creation of the RD53A local database user.
-   Creation of the RD53A local database chip configuration.
-   Running scans as usual but with database upload.

BDAQ-based system
-----------------

Follow instructions [here](https://gitlab.cern.ch/silab/bdaq53).

TODO
