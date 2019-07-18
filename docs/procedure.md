Overview
=========
This page will cover the full testing procedure expected of sites receiving the traveling module.
The procedure consists of:

   * [Reception inspection](#recInsp)
   * Basic communication
   * Trim IREF and voltage regulators
   * Scans (including pre-tune scans, tuning, and post-tuning scans) & plotting

There is a checklist at the end of this page, (and attached as a pdf) to keep track of all the tasks which might be useful to print out whilst testing.   
   
<a id="recInsp"></a>Reception inspection
======================
These basic tasks should be performed upon recieving the package:

   1. Please note in the table, [here](https://twiki.cern.ch/twiki/bin/viewauth/Atlas/ContactDetails) when the module was recieved.
   2. Please take photos of the package, as well as performing a visual inspection of the module, being careful to note down (and photograph) any scratches or damage on the board. In addition, please check the wire bond connections under a microscope to make sure there is no detachment during transport.
   3. Check that the jumpers on the Single Chip Card (SCC) are correct. In particular, 
      * <span style="color:red">The pin headers labelled `PWR_A` and `PWR_D` (outlined in red box in image) should both be set to `VINA` and `VIND`, respectively. This is done by setting the jumper to connect the left and middle pin for each set of three pins (when the board is orientated as seen in the photo). Setting these jumpers ensures the voltage regulators are used during operation. Setting these incorrectly could lead to permanent damage in the chip.</color> 
      * Check that the PLL and CML drivers are being powered from VDDA by setting VDD_PLL_SEL and VDD_CML_SEL to VDDA, respectively (left most pins for each set of 6 in yellow box in photo).  
      * Make sure, for normal operation, that both the `VREF_ADC` and `IREF_IO` pin headers both have jumpers on them.
      * Ensure that there are jumpers solder to pads `JP10` and `JP11`. 
      * Finally, ensure that there is a jumper across the `PLL_RST` pin header.

        ![pins](images/SCC_JumperConfiguration_edited.jpg)
    

Testing Parameters
===============
We try to provide supplementary information here, please refer to existing documentations. If anything is missing on both sides, feedback would be appreciated.

-	On module reception always check/set the correct configuration of the
	jumpers on the single chip card. Please cross-check the configuration of
	the SCC with [this document](https://twiki.cern.ch/twiki/pub/RD53/RD53ATesting/RD53A_SCC_Configuration.pdf) or [here](https://yarr.readthedocs.io/en/latest/rd53a).

-	Tests should be done at room temperature with the chip powered in **LDO**
	mode at **1.8V**. (In direct powering mode use maximum 1.3V, anything higher will likely to
	result in permanent damage.)
	
-	BDAQ and YARR use different default chip configurations. For a better comparability they are modified with
	[5uA inner layer parameters](https://twiki.cern.ch/twiki/bin/viewauth/RD53/RD53ATesting#Guidelines_for_Front_ends).
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
	- For BDAQ: change ``VREF_A_TRIM`` and ``VREF_D_TRIM``.

-	All three FE on the RD53A module is advised to be tuned. The tuning
	protocol is shown below. 
	The threshold of all three FE can be tuned to
	**1000e**. This is the recommended value for the travelling module. The ToT
	should be tuned to **8BC** at **10000e**.


Testing with YARR
=====================

Use the [scanConsole](https://yarr.readthedocs.io/en/latest/scanconsole) for all tunings and scans following [this tuning routine](https://yarr.readthedocs.io/en/latest/rd53a#tuning-routine).
Run each scan and tuning **by hand**, observe the output in the terminal and look at the plots after scanConsole is finished. Look into the chip configuration and make sure the threshold DAC for each frontend makes sense.  
Please use the [ROOT scripts](https://yarr.readthedocs.io/en/latest/rootscripts) (Threshold and NoiseMap) to produce fitted plots which show separate the data for each FE in pdf format and for all pixels in differential frontend.



Testing with BDAQ
=====================

Follow instructions
[here](https://gitlab.cern.ch/silab/bdaq53/wikis/User-guide/General-usage).
You can either execute with e.g. ``bdaq53 scan_digital`` or
``python scan_digital.py``.

Once made sure that the module works, tune all FEs
and save the results before and after tuning. For FE specific scans and
tunings, adjust ``'start_column'`` and ``'stop_column'`` in the scan code
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


Detailed instructions:
-------------------------------------------

### Preparing the module

Connect the DP1 connector on the single chip card (SCC) to the “DP_ML 1”
connector on the BDAQ board using a standard DisplayPort (DP) cable.  

Make sure the SCC is jumpered for the correct powering mode and your power supply
is setup accordingly.

Observe the BDAQ board. On the FPGA daughterboard there should be 4 LEDs labeled 0-3. LEDs 0 and 1 should be lit up, while LED 3 should be off and LED 4 should be flashing. Once you turn on the powersupply of the SCC, LED4 should stop flashing and either turn off permanently or all four LEDs should be constantly on.

### Trimming your chip

In order to have your chip working at optimal conditions, you have to trim IREF, VREF_A and VREF_D, as well as VREF_ADC. IREF is the reference current for all DACs on the chip. VREF_A/D are the regulator reference voltages, which determine the analog and digital supply voltage of the chip (VDDA and VDDD) that will be generated by the regulators in (shunt-)LDO mode. VREF_ADC is the reference voltage for the internal ADC circuit as well as the charge injection circuit. If this reference is not trimmed correctly, the chip charge calibration and therefore the electron scale in any plot will be wrong! You can acquire these settings by either using the ``calibrate_vref.py`` and ``calibrate_vref_adc.py`` routines of BDAQ53 or manual trimming (see [wiki]( https://gitlab.cern.ch/silab/bdaq53/wikis/User-guide/Trimming-VREF)).


### Preparing the module configuration file

Download the default chip configuration file from above and make a copy of it, naming it according to the chip you are testing. For example, if you have travelling module #1 with chip serial number 0x0494, name your copy ``0x0494.cfg.yaml``. Open your freshly created copy and enter the optimal trimbit settings you acquired in the last step in the trim section of the file.
Make sure that the global threshold DACs are set to a safe threshold of >3000e: e.g. VTH_SYNC: 390, Vthreshold_LIN: 415, VTH1_DIFF: 600.
The file will be automatically picked up if its name matches the chip serial number you enter into testbench.yaml in the next step. 


### Preparing the output directory
Create a directory on your PC that will be used for all BDAQ53 output files. Open ``bdaq53/bdaq53/testbench.yaml`` with any text editor and in the **general section**, set

- chip_sn to the serial number of the chip / module you are going to test,
- output_directory to the directory you just created.
- Make sure, chip_configuration is set to ``‘auto’``.

Copy the configuration file you downloaded or created in the previous step to the output directory. This way, the configuration file is used for the very first scan. After that, the configuration is passed through consecutive scans.

## Testing the setup
To make sure everything works as expected, test the setup by changing to ``bdaq53/bdaq53/scans`` and opening ``scan_digital.py``. Verify that the region of interest is defined as  
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
Check the output: In the very beginning it should tell you which chip configuration file it is using. Verify that this is the file you downloaded or created in the previous section. Let the scan finish and open the output .pdf file. Double check that the correct chip serial number is displayed in the first sentence on the first page. Scroll to the second page. The **Event status** histogram should be empty. Scroll to the third page. The **Occupancy** map should be homogeneously yellow, showing an occupancy of 100 hits for every pixel. The total amount of hits should be \sum = 7680000, or 76800 pixels with 100 hits each.
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
For YARR, plot threshold and noise distributions with ROOT scripts.
