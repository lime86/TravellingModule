Introduction
============

Site commissioning will start with introduction of the "Travelling
Module". The main purpose of the "Travelling Module" exercise is to make
sure that every potential commissioning site is familiar with the basic
operation of the RD53A chip with either YARR or BDAQ setups and the
results from the essential tuning protocols match the results of other
sites. Common chip sent around should help unify setups across the
institutes and help everyone to get up and running while ensuring
consistent results.

Structure of this documentation
=================================
This readTheDocs should be followed sequentially for new institutes. 
**If you are already have an established SCC testing site, please briefly review the experimental setup, but feel free to skip ahead to the Testing Procedure**.

Documentation structure:

   - **Travelling modules**: Overview of the three travelling modules, including photos
   - **Commissioning specification**: Minimum requirements for assembly site
   - **Experimental setup**: Ovewrview of power supplies needed and readout options
   - **FPGA configuration**: The RD53 chip on the Single Chip Card (SCC) is communicated with via an FPGA in both YARR and BDAQ. This guide will direct for instructions on how to configure both devices.
   - **Readout software installation**: How to install both YARR and BDAQ. Also contains links to each project's documenation.
   - **Testing procedure**: All the tests, scans, and checks to run on the travelling module. 
   - **Data storage**: Where to put the testing results when you're done.


Information and Support
=======================
##RD53A


For RD53A specific questions please consult the [testing
twiki](https://twiki.cern.ch/twiki/bin/viewauth/RD53/RD53ATesting). There is also a Mattermost team on [RD53A Testing](https://mattermost.web.cern.ch/rd53-testing).

##Travelling Module

There is an ITkPixel Mattermost team with a channel on the travelling
module for quick support. Join
[here](https://mattermost.web.cern.ch/signup_user_complete/?id=ujzsdu51p3nuirqp7h5bkjo5ay).

##YARR

Please use release v1.0.0 (master branch).
General YARR documentation can be found on
[readthedocs](https://yarr.readthedocs.io). For YARR specific questions
and problems there is a [Mattermost
channel](https://mattermost.web.cern.ch/yarr) for discussions.

##BDAQ
Please use ``travelling_module`` branch.
Instructions can be found
[here](https://gitlab.cern.ch/silab/bdaq53) with additional information
on the [wiki](https://gitlab.cern.ch/silab/bdaq53/wikis/home).

Contact details
===============

- You can find the participating institutes and their contact details on the [sign-up sheet](https://docs.google.com/spreadsheets/d/1qtbo60B43QQgahlq0hG3hi0f7tpFaO4p044CMa54tGE/edit#gid=0), which is closed for editing, but commenting is still possible.
- The current schedule can be found [here](https://docs.google.com/spreadsheets/d/1uaxTqf-mSaBd6_UuOKpe0N2RLMPN3AFnNkIQ4CnIEUY/edit?usp=sharing). There is also a copy of the contact information of the participating institutes. Please check for the correctness and if necessary, provide feedback to Lingxin. <span style="color:red">We will encounter delays. If experienced institutes finish with the tests earlier, please post the chip straight away to the next institute.</span>  
- On "Travel Pack" reception, please fill the table
[here](https://twiki.cern.ch/twiki/bin/view/Atlas/ContactDetails). Also
review the table once you completed work with the "Travelling Module".

