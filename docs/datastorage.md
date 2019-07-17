Data Storage
============

The final tuning data of the travelling chips and modules should be stored in a common database. For the moment it is a CERNbox as described below.
If you used YARR, please produce ROOT plots using the provided plotting scripts and upload them as well.

Final full set of data to be uploaded:

- Pre-tuning scans
- Tunings
- Post-tuning scans
- Temperature monitoring data ([data sheet of the NTC on the SCC](https://www.mouser.de/datasheet/2/362/ktthermistor-3035.pdf))
- Notes on power consumption of the chip before and after configuration
- A file with additional comments
- Anything else you think might be important	

CERNbox
-------

The CERNbox (1TB) ```/eos/project/a/atlas-itk-pixel-module/``` is accessible via lxplus.  
User should subscript to egroups "cernbox-project-atlas-itk-pixel-module-readers" and "cernbox-project-atlas-itk-pixel-module-writers"
for read and write access (no CERN account needed in principle). However, as for mysterious reason we don't get any notifications if anyone signs up,
please drop an email to Lingxin so your request can be approved. Following the approval 40 minutes is needed for all caches to be updated.


All the members of the following 2 e-groups have the respective access to the project space:

- cernbox-project-atlas-itk-pixel-module-readers (anyone in this egroup can read in the project space)
- cernbox-project-atlas-itk-pixel-module-writers (anyone in this egroup can read, write and delete in the project space)
 
The following 2 folders are pre-created:

- /eos/project/a/atlas-itk-pixel-module/www/ (folder for hosting an EOS-site-type website)
- /eos/project/a/atlas-itk-pixel-module/public/ (public folder for all CERN authenticated users)
 
Members of the eos project "atlas-itk-pixel-module" (cernbox-project-atlas-itk-pixel-module, not the working group mailing list) also have the option of going to their CERNBox (via a web browser) to see the project files
(go to 'Your projects' and select 'project atlas-itk-pixel-module'). Users need to login to <https://cernbox.cern.ch> ONCE to activate their CERNBox space!

Folder structure:

```bash
.
|-- public
|-- www
|-- TravellingModule 
    |-- chip#1
		|-- BDAQ
			|-- institute#b1 : where institute#b1 stores the data on this chip
			|-- ...
			`-- institute#bn
		`-- YARR
			|-- institute#y1 : where institute#y1 stores the data on this chip
			|-- ...
			`-- institute#yk
    |-- chip#2
		|-- BDAQ
			|-- institute#bn+1 : where institute#bn+1 stores the data on this chip
			|-- ...
			`-- institute#bn+m
		`-- YARR
			|-- institute#yk+1 : where institute#yk+1 stores the data on this chip
			|-- ...
			`-- institute#yk+j
    |-- chip#3
		|-- BDAQ
			|-- institute#bn+1 : where institute#bn+1 stores the data on this chip
			|-- ...
			`-- institute#bn+m
		`-- YARR
			|-- institute#yk+1 : where institute#yk+1 stores the data on this chip
			|-- ...
			`-- institute#yk+j
    |-- module#1
    |-- module#2 
    `-- module#3 
`-- some other ITk pixel module project
```

