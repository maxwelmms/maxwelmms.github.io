# Hardware Management Console (HMC)

## Root/unrestricted shell HMC

Ref: [pesh command](https://www.ibm.com/docs/en/power8/8335-GCA?topic=HW4L4/p8edm/pesh.htm)

**pesh** provides full shell access to the HMC for product engineering and support personnel. pesh takes the serial number of the HMC machine or unique ID of the virtual HMC where full shell access is requested, then prompts the user for a one day password obtained from the support organization. If the password is valid, the user is granted full shell access. Only the hscpe user can run this command. 


To obtain full shell access to a Hardware Management Console (HMC): 
**pesh** serial-number-of-HMC-machine 

To obtain full shell access to a virtual HMC: 
**pesh** unique-ID-of-virtual-HMC


On an HMC machine, run the lshmc -v command to list the Vital Product Data (VPD) information: 
**lshmc -v**

Pass the serial number following the SE tag to the pesh command: 
**pesh 10DA45C** 
You will be prompted for a password. 

On a virtual HMC, run the lshmc -v command to list the Vital Product Data (VPD) information: 
**lshmc -v** 

Pass the unique ID following the UVMID tag with or without the : 
separators to the pesh command: 
**pesh 4c7f:459c:4980:bef5** 
or 
**pesh 4c7f459c4980bef5** 
You will be prompted for a password. 



## Free up space in HMC file systems

Ref: [chhmcfs command](https://www.ibm.com/docs/en/power9?topic=commands-chhmcfs)

**chhmcfs** frees up space in Hardware Management Console (HMC) file systems. Space is freed by removing temporary HMC files that are used for HMC and managed system firmware problem analysis from the HMC hard disk. 
This command can free up space in the following file systems: **/var**, **/var/hsc/log**, **/dump**, **/extra**, **/data**, and **/**. The temporary files that can be removed from the **/var** and **/var/hsc/log** file systems include HMC trace and log files. The temporary files that can be removed from the **/dump** file system include managed system dumps, managed frame dumps, and debug data collected using the HMC **pedbg** command. The temporary files that can be removed from the /extra file system include managed system dumps and managed frame dumps. The temporary files that can be removed from the /data file system include HMC Java core dump and heap dump files, and service files called home with serviceable events. 
**This command will not remove temporary HMC trace and log files that are in use.**


 **EXAMPLES**

	#Remove temporary HMC files which have not been modified during the last day (24 hours) from all file systems: 
	chhmcfs -o f -d 1
	#Remove all temporary HMC files from all file systems: 
	chhmcfs -o f -d 0
	#Remove temporary HMC files which have not been modified during the last 36 hours from the /var file system: 
	chhmcfs -o f -h 36 -f /var
	#Remove temporary HMC files from the /dump file system to free up to 100 MB: 
	chhmcfs -o f -s 100 -f /dump



-------------------------------------------------------------------------------------------------------------

Ref: [lshmcfs command](https://www.ibm.com/docs/en/power9/9223-22S?topic=commands-lshmcfs)

**lshmcfs** lists Hardware Management Console (HMC) file system disk space usage information. Disk space usage information is listed for the HMC file systems that can contain temporary HMC files used for HMC and managed system firmware problem analysis. 
This command lists information for the following file systems: **/var**, **/var/hsc/log**, **/dump**, **/extra**, **/data**, and **/**. The temporary files in the **/var** and **/var/hsc/log** file systems include HMC trace and log files. The temporary files in the **/dump** file system include managed system dumps, managed frame dumps, and debug data collected using the HMC **pedbg** command. The temporary files in the /extra file system include managed system dumps and managed frame dumps. The temporary files in the **/data** file system include HMC Java core dump and heap dump files, and service files called home with serviceable events. 
All size and free space values displayed by this command are in megabytes.


**EXAMPLES**

	#List current HMC file system disk space usage information: 
	lshmcfs
	#List HMC file system disk space usage information if temporary HMC files which have not been modified during the last 2 days (48 hours) were removed: 
	lshmcfs -o c -d 2
	#List HMC file system disk space usage information if all temporary HMC files, except the trace and log files that are in use, were removed: 
	lshmcfs -o c -d 0
	#List HMC file system disk space usage information if temporary HMC files were removed to free up to 100 MB in each file system: 
	lshmcfs -o c -s 100
