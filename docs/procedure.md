Testing Parameters
===============
We try to provide supplementary information here, please refer to existing documentations. If anything is missing on both sides, feedback would be appreciated.

-	On module reception always check/set the correct configuration of the
	jumpers on the single chip card. Please cross-check the configuration of
	the SCC with [this document](https://twiki.cern.ch/twiki/pub/RD53/RD53ATesting/RD53A_SCC_Configuration.pdf) or [here](https://yarr.readthedocs.io/en/devel/rd53a/).

-	Tests should be done at room temperature with the chip powered in **LDO**
	mode at **1.8V**. (In direct powering mode use maximum 1.3V, anything higher will likely to
	result in permanent damage.)
	
-	Please use the default configuration provided by the software release with [5uA inner layer parameters](https://twiki.cern.ch/twiki/bin/viewauth/RD53/RD53ATesting#Guidelines_for_Front_ends).
	The modified chip configurations can be downloaded for YARR: [rd53a_TravellingChip.json](files/rd53a_TravellingChip.json) and for BDAQ: [rd53a_TravellingChip.cfg.yaml](files/rd53a_TravellingChip.cfg.yaml)
	The only registers that should be changed in the chip configuration file are
	- IREF (according to waferprobing data, via jumper and trim bits)
	- VOLTAGE_TRIM (according to waferprobing data and measurements of VDDA and VDDD pins)
	- MON_BG_TRIM (according to waferprobing data and measurement of )
	- VTH_SYNC, VThreshold_LIN, VTH1/2_DIFF (by threshold tuning procedure)
	- IBIAS_KRUM_SYNC, KRUM_CURR_LIN, VFF_DIFF (by ToT tuning procedure)  	
	- Please change ```"Name": "JohnDoe",```(YARR) or ```chip_sn: '0x0000'```(BDAQ) according to the chip you test.

-	Check that Iref is set to 4.0 μA: Remove the jumper labeled IREF IO,
	power up the chip and measure the current between these pins with e.g. a Keithley source meter. If necessary,
	adjust the 4-bit IREF TRIM jumpers. Remember to put back the IREF IO jumper for operation.

-	Measure **VDDA** and **VDDD** on the SCC and set them to **1.2V** in the according entries in the chip configuration file.
	- For YARR: change `SldoAnalogTrim` and `SldoDigitalTrim`. If you still get ```data not valid``` errors, adjust VDDA to a value that this error disappears. More information in [FAQ & Troubleshooting](../troubleshooting).
	- For BDAQ: change `VREF_A_TRIM` and `VREF_D_TRIM`.

-	All three FE on the RD53A module is advised to be tuned. The tuning
	protocol is shown below. 
	The threshold of all three FE can be tuned to
	**1000e**. This is the recommended value for the travelling module. The ToT
	should be tuned to **8BC** at **10000e**.


Testing with YARR
=====================

Use the [scanConsole](https://yarr.readthedocs.io/en/devel/scanconsole/) for all tunings and scans following [this tuning routine](https://yarr.readthedocs.io/en/devel/rd53a/#tuning-routine).
After scans and tunings a set of [ROOT scripts](https://yarr.readthedocs.io/en/devel/rootscripts/) can be used to produce pretty plots and separate the data for each FE.



Testing with BDAQ
=====================

Follow instructions
[here](https://gitlab.cern.ch/silab/bdaq53/wikis/User-guide/General-usage).
You can either execute with e.g. `bdaq53 scan_digital` or
`python scan_digital.py`.

Once made sure that the module works, tune all FEs
and save the results before and after tuning. For FE specific scans and
tunings, adjust `'start\_column'` and `'stop_column'` in the scan code
accordingly.

For any tuning, the electron equivalence of injected charge is roughly
10 times the difference between `VCAL_MED` and `VCAL_HIGH`. Pay
attention to the scanning range and adjust `VCAL_HIGH_start` and
`VCAL_HIGH_stop` in the `local_configuration` section of the scan code
accordingly.

Start with a clean data folder, make sure you don't have old mask files
in your folder. The same mask file is going to be written and rewritten
for each FE step.

Pixel threshold tuning uses ```meta_tune_local_threshold.py```.


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
2.	pixel threshold tuning
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
