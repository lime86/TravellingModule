Experimental Setup
==================

Experimental setups will inevitably differ from site to site depending
on equipment availability. It is recommended for each organisation to
create a page on this Twiki and describe their setup in a free form in
as much detail as practically needed. General considerations are as
follows.

For the chip:

-   Good quality dual / triple channel laboratory power supply capable
    of providing 1.8V @ 1A on each channel.
-   1-2m long custom made cable with a 4-pin Molex connector to power
    the chip.
-   1-2m long DisplayPort to DisplayPort (Mini DisplayPort) to
    connect the chip to BDAQ (YARR) readout.
-   Modern PC with &gt; 8 GB RAM, Quad-core CPU, 1TB HD running CentOS 7
    is highly recommended. ```sudo``` rights are required for FPGA programming.

In addition for the module:

-   High voltage power supply, e.g. Keithley 2410.
-   Single pin Lemo cable with 00 connector to bias the sensor.

Details of setups at each site can be found below:

-   [University of
    Glasgow](CharacterisationSetups#University_of_Glasgow)
    

YARR
----




BDAQ
----
Dedicated BDAQ hardware setup can be found [here](https://gitlab.cern.ch/silab/bdaq53/wikis/home#hardware-setup).

(to be updated)  
To power the BDAQ board, you can use either USB or a dedicated 5V powersupply. Select the powering method accordingly with the jumper next to the VDC input on the board. When using USB, also a USB 2.0 cable is fine, but the USB powersupply or port has to provide at least 1A of current.
Connect the BDAQ53 base board to the readout PC using a standard Ethernet cable (>= CAT6). For the best experience, use an additional ethernet interface on your PC (either PCIe or USB3, though it has to be 1000BASE-T – Gigabit ethernet) and the “ETH” port on the BDAQ board next to the USB3 port.
