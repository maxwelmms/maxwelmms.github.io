# [IBM Support](https://www.ibm.com/mysupport/s/?language=en_US)

## System logs and data

### [SNAP](https://www.ibm.com/docs/en/aix/7.2?topic=s-snap-command)

    -a                copies all system config. information to /tmp/ibmsupt directory tree
    -c                creates a  compressed tar image (snap.tar.Z) of all files in the /tmp/ibmsupt
    -g                gather general information
    -e                for HACMP, it runs clverification and gathers the data creating a snap


**EXAMPLES:**

	#removes old snap from /tmp/ibmsupt
	snap -r

	#creates a new snap file
	snap -gc



**Reading a compressed snap file:**

	#creates a compressed snap file (/tmp/ibmsupt/snap.pax.Z)
	snap -ac

	#uncompresses it, we will have a snap.pax file
	uncompress snap.pax.Z

	#unpack files, after files can be read
	pax -rvf snap.pax


**Extracting snap.pax.Z file:**

For basic dump analysis, this article is mostly interested in a dump image. Here, we cover how to extract the appropriate files from the snap package and then explain a methodical approach to examine the dump, and find the fundamental reason for a system crash. The dump file and the UNIX® file are in the dump subdirectory of the snap package.

Though we are primarily focused on the dump image, it is important to note that snap can provide you with useful information when used with appropriate options. Additional information is found in the General and Kernel subsections of the article.

**General**

This general directory includes information about the system runtime environment, for example:

    Copy of ODM data.
    All environment variables (e.g., PATH and TZ).
    Date and time the data was collected.
    Amount of real memory on the system (bootinfo -r).
    Listing of all defined paging spaces.
    Listing of all installed filesets and their levels.
    Listing of all installed APARs.
    Device attributes (lsattr -El).
    System VPD information (lscfg -pv).
    Status of last dump (sysdumpdev -L).

**Kernel**

The kernel subdirectory contains useful kernel information (Process and memory data).

    Date and time the data was collected
    Vmstat output
    VMM tunable information (vmo -L).
    Scheduling tunable information (schedo -L).
    I/O related tunable iformation (ioo -L).
    Environment variables.
    SRC information (lssrc -a).
    Process information (ps -ef and ps -leaf).
    Checksum of device drivers and methods.

**Extracting the snap package:**

The pax command is used to extract files from the snap package.

    #To view the contents of a snap package, type:
    zcat snap.pax.Z | pax -v

    #To extract the entire contents of a package, type:
    zcat snap.pax.Z | pax -r

    #To extract just the dump, general, and kernel subdirectories, type:
    uncompress snap.pax.Z
    zcat snap.pax.Z | pax -r ./dump ./general ./kernel
