Testing Parameters
===============
We try to provide supplementary information here, please refer to existing documentations. If anything is missing on both sides, feedback would be appreciated.

-	On module reception always check/set the correct configuration of the
	jumpers on the single chip card. Please cross-check the configuration of
	the SCC with [this document](https://twiki.cern.ch/twiki/pub/RD53/RD53ATesting/RD53A_SCC_Configuration.pdf) or [here](https://yarr.readthedocs.io/en/latest/rd53a).

-	Tests should be done at room temperature with the chip powered in **LDO**
	mode at **1.8V**. (In direct powering mode use maximum 1.3V, anything higher will likely to
	result in permanent damage.)
	
-	Please use the default configuration provided by the software release with [5uA inner layer parameters](https://twiki.cern.ch/twiki/bin/viewauth/RD53/RD53ATesting#Guidelines_for_Front_ends).
	The modified chip configurations can be downloaded for YARR: [rd53a_TravellingChip.json](files/rd53a_TravellingChip.json) and for BDAQ: [rd53a_TravellingChip.cfg.yaml](files/rd53a_TravellingChip.cfg.yaml)
	The only registers that should be changed in the chip configuration file are
	- IREF (according to waferprobing data, via jumper and trim bits)
	- VOLTAGE_TRIM (according to waferprobing data and measurements of VDDA and VDDD pins)
	- MON_BG_TRIM (according to waferprobing data and measurement of <span style="color:red">todo</span>)
	- VTH_SYNC, VThreshold_LIN, VTH1/2_DIFF (by threshold tuning procedure)
	- IBIAS_KRUM_SYNC, KRUM_CURR_LIN, VFF_DIFF (by ToT tuning procedure)  	
	- Please change ``"Name": "JohnDoe",``(YARR) or ``chip_sn: '0x0000'``(BDAQ) according to the chip you test.

-	Check that Iref is set to 4.0 μA: Remove the jumper labeled IREF IO,
	power up the chip and measure the current between these pins with e.g. a Keithley source meter. If necessary,
	adjust the 4-bit IREF TRIM jumpers. Remember to put back the IREF IO jumper for operation.

-	Measure **VDDA** and **VDDD** on the SCC and set them to **1.2V** in the according entries in the chip configuration file.
	- For YARR: change ``SldoAnalogTrim`` and ``SldoDigitalTrim``. If you still get ``data not valid`` errors, adjust VDDA to a value that this error disappears. More information in [FAQ & Troubleshooting](../troubleshooting).
	- For BDAQ: change ``VREF_A_TRIM` and `VREF_D_TRIM``.

-	All three FE on the RD53A module is advised to be tuned. The tuning
	protocol is shown below. 
	The threshold of all three FE can be tuned to
	**1000e**. This is the recommended value for the travelling module. The ToT
	should be tuned to **8BC** at **10000e**.


Testing with YARR
=====================

Use the [scanConsole](https://yarr.readthedocs.io/en/latest/scanconsole) for all tunings and scans following [this tuning routine](https://yarr.readthedocs.io/en/latest/rd53a#tuning-routine).
Run each scan and tuning **by hand**, observe the output in the terminal and look at the plots after scanConsole is finished. Look into the chip configuration and make sure the threshold DAC for each frontend makes sense.
After scans and tunings a set of [ROOT scripts](https://yarr.readthedocs.io/en/latest/rootscripts) can be used to produce pretty plots and separate the data for each FE.



Testing with BDAQ
=====================

Follow instructions
[here](https://gitlab.cern.ch/silab/bdaq53/wikis/User-guide/General-usage).
You can either execute with e.g. ``bdaq53 scan_digital`` or
``python scan_digital.py``.

Once made sure that the module works, tune all FEs
and save the results before and after tuning. For FE specific scans and
tunings, adjust ``'start\_column'`` and ``'stop_column'`` in the scan code
accordingly.

For any tuning, the electron equivalence of injected charge is roughly
10 times the difference between ``VCAL_MED`` and ``VCAL_HIGH``. Pay
attention to the scanning range and adjust `VCAL_HIGH_start` and
``VCAL_HIGH_stop`` in the ``local_configuration`` section of the scan code
accordingly.

Start with a clean data folder, make sure you don't have old mask files
in your folder. The same mask file is going to be written and rewritten
for each FE step.

Pixel threshold tuning uses ``meta_tune_local_threshold.py``.


Additional instructions (to be cleaned up):
-------------------------------------------

Preparing the module
--------------------
Connect the DP1 connector on the single chip card (SCC) to the “DP_ML 1” connector on the BDAQ board using a standard DisplayPort (DP) cable.
Make sure the SCC is jumpered for the correct powering mode and your powersupply is setup accordingly. Also double check if the IREF header is jumpered correctly according to this [list](TODO).
Observe the BDAQ board. On the FPGA daughterboard there should be 4 LEDs labeled 0-3. LEDs 0 and 1 should be lit up, while LED 3 should be off and LED 4 should be flashing. Once you turn on the powersupply of the SCC, LED4 should stop flashing and either turn off permanently or all four LEDs should be constantly on.
Preparing the module configuration file
Download the module specific configuration file from [here](TODO). Verify that the chip serial number and trimbit settings are correct according to this [list](TODO). Alternatively you can create the configuration file yourself by creating a copy of bdaq53/bdaq53/rd53a_default.cfg.yaml, renaming it for example to 0x1234.cfg.yaml and changing chip_sn, VREF_A_TRIM, VREF_D_TRIM and MON_BG_TRIM according to the list above. The latter three of these parameters are the optimal voltage trimbit settings for this chip. 
Preparing the output directory
Create a directory on your PC that will be used for all BDAQ53 output files. Open bdaq53/bdaq53/testbench.yaml with any text editor and in the general section, set
    • chip_sn to the serial number of the chip / module you are going to test,
    • output_directory to the directory you just created.
    • Make sure, chip_configuration is set to ‘auto’.
Copy the configuration file you downloaded or created in the previous step to the output directory. This way, the configuration file is used for the very first scan. After that, the configuration is passed through consecutive scans.
Testing the setup
To make sure everything works as expected, test the setup by changing to bdaq53/bdaq53/scans and opening scan_digital.py. Verify that the region of interest is defined as  
```yaml
	'start_column': 0,
	'stop_column': 400,
	'start_row': 0,
	'stop_row': 192,
```
This means that the whole pixel matrix will be scanned. Start the scan by running
```bash
	$ python scan_digital.py
```
Check the output: In the very beginning it should tell you which chip configuration file it is using. Verify that this is the file you downloaded or created in the previous section. Let the scan finish and open the output .pdf file. Double check that the correct chip serial number is displayed in the first sentence on the first page. Scroll to the second page. The Event status histogram should be empty. Scroll to the third page. The Occupancy map should be homogeneously yellow, showing an occupancy of 100 hits for every pixel. The total amount of hits should be  = 7680000, or 76800 pixels with 100 hits each.
Congratulations, you are ready to begin testing the module.


Tuning protocol
===============

Pre-tuning scans
----------------
For all frontends (can be FE specific if the column range changed
accordingly in the code):

-   digital scan
-   analog scan
-   threshold scan

Tunings
-------
For each frontend separately. The tuning of the linear frontend has to start with
2000e and retuned to 1000e (execute step 1 and 2 with 2000e and repeat with 1000e).

1.	global threshold tuning
2.	pixel threshold tuning (not for syncFE)
3.	time over threshold tuning
4.	re-adjust pixel threshold

Post-tuning scans
-----------------
For all frontends (can be FE specific if the column range changed
accordingly in the code):

-	threshold scan
-	ToT scan

Post processing
---------------
For YARR, plot threshold and noise distributions with root scripts.
