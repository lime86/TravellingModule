Programme FPGA
==============

To programme the FPGA both for YARR and BDAQ system, Vivado is required and can be [downloaded for
free](https://www.xilinx.com/support/download.html) (registration
needed) as either Vivado Webpack or Vivado Lab.

YARR
----
For YARR follow [this link](https://github.com/Yarr/Yarr-fw/blob/master/syn/xpressk7/README.md).



BDAQ
----
For BDAQ follow [this
link](https://gitlab.cern.ch/silab/bdaq53/wikis/Hardware/fpga-configuration).

Additional instructions: (to be updated)

First, make sure Xilinx Vivado is installed on your system. Connect the BDAQ board to the PC via USB (USB 2.0 is enough).
Next, download the travelling module firmware from TODO.
The firmware can flashed using a simple command:
```bash
	# bdaq53 --firmware [PATH-TO-BITFILE]
```
Alternatively, use Xilinx Vivado to flash (the preferred method is to flash the FPGA persistently using the .mcs file) to the FPGA using the USB interface of the BDAQ base board. More instructions for manual flashing can be found [here]( https://gitlab.cern.ch/silab/bdaq53/wikis/Hardware/FPGA-configuration#permanent-configuration)

Testing the connection
Configure the network interface on your computer, that the BDAQ board is connected to as follows:
	IP Address: 192.168.10.10
	Subnet Mask: 255.255.255.0
	Gateway: 0.0.0.0
by using
```bash
sudo ifconfig enx00e04c68000a 192.168.10.10 netmask 255.255.255.0
```

Make sure, no jumper is set on the “PMOD” header on the BDAQ board. See if the communication between the PC and the board works by running
```bash
	ping 192.168.10.12
```
