# Logical Partition (LPAR)

## Profile types and architecture

### CPU
- **Dedicated:** The PU is assigned to the LPAR in the Shared Processor Pool.
- **Dedicated Donating:** Flexibility to donate idle or spare processors owned by a dedicated LPAR to a shared processor pool.
- **Shared Uncapped:**
	- Processing Units (PU):
		- Configure the desired number of Processing Units (PUs) to support average off-peak utilization +20%.
	- Virtual Processor (VP):
		- Configure enough Virtual Processors (VPs) to handle processing spikes.
- **Shared Capped:**
	- Processing Units (PU):
		- Configure the number of Processing Units (PU) for peak times + 20%.
	- Virtual Processor (VP):
		- Set desired Virtual Processors (VPs) to the next integer after the number of Processing Units (PUs).
- **Both:**
	- The EC/VP ratio should be around 0.6 and 0.7.

- **Weight:** Sorts by priority (weight) the LPARs that will use the Shared Processor Pool so that they can make use of virtual processors.
	- All client LPARs are weighted equally, and the recommendation is to prioritize loans in the SPP.
	- Example: VIOS=255 / PRD=180-200 / QAS,DEV=128-160.
- **Entitlement:**
	- **Desired:** Number of processors allocated to a given LPAR.
	- **Max**: Maximum number of processors that can be dynamically adjusted through a procedure via HMC (DLPAR), Dynamic
Logical Partitioning.
- **Desired Proc:** Number of virtual processors allocated to a given LPAR to cover processing spikes. The number of additional vCPUs will
be borrowed from the Shared Processor Pool. (SPP)
- **SMT:** The number of "threads" (Simultaneous Multi-Thread) is multiplied with the number of virtual processors allocated,
generating the "Logical CPUs”. The load in the Logical CPUs should be considered in case of EC or VP changes.

