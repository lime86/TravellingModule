FPGA Configuration
==================

To programme the FPGA both for YARR and BDAQ system, Vivado is required
and can be `downloaded for
free <https://www.xilinx.com/support/download.html>`__ (registration
needed) as either Vivado Webpack or Vivado Lab.

YARR
----

Instructions on how to flash the firmware can be found
`here <https://github.com/Yarr/Yarr-fw/blob/master/syn/xpressk7/README.md>`__.
A brief firmware guide and modification of the Ohio card can be found
`here <https://yarr.readthedocs.io/en/latest/fw_guide>`__

BDAQ
----

For the travelling module a frozen firmware version 0.13 is used and can
be found at the end of `this
list <https://gitlab.cern.ch/silab/bdaq53/wikis/Hardware/Firmware-(development-versions)>`__
or downloaded here:
`v0.13.0\_travelling\_module\_BDAQ53\_1LANE\_RX640.tar.gz <https://gitlab.cern.ch/silab/bdaq53/wikis/uploads/e27b7af2ca9c12d6072628e8ddec592c/v0.13.0_travelling_module_BDAQ53_1LANE_RX640.tar.gz>`__.
For detailed instructions on FPGA configuration follow `this
link <https://gitlab.cern.ch/silab/bdaq53/wikis/Hardware/fpga-configuration>`__.

Quick guide
~~~~~~~~~~~

Connect the BDAQ board to the PC via USB (USB 2.0 is enough). Next,
`download the frozen travelling module
firmware <https://gitlab.cern.ch/silab/bdaq53/wikis/uploads/e27b7af2ca9c12d6072628e8ddec592c/v0.13.0_travelling_module_BDAQ53_1LANE_RX640.tar.gz>`__.
The firmware can flashed using a simple command:

.. code:: bash

    $ bdaq53 --firmware [PATH-TO-BITFILE]

Alternatively, use Xilinx Vivado to flash (the preferred method is to
flash the FPGA persistently using the .mcs file) to the FPGA using the
USB interface of the BDAQ base board.

Testing the connection
~~~~~~~~~~~~~~~~~~~~~~

Configure the network interface on your computer, that the BDAQ board is
connected to as follows:

::

    IP Address: 192.168.10.10  
    Subnet Mask: 255.255.255.0  
    Gateway: 0.0.0.0  

by using

.. code:: bash

    $ sudo ifconfig <your ethernet interface> 192.168.10.10 netmask 255.255.255.0

Make sure, no jumper is set on the “PMOD” header on the BDAQ board. See
if the communication between the PC and the board works by running

.. code:: bash

        ping 192.168.10.12
