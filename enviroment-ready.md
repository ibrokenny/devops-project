# Enviroment Verification --- 30 Minute Session 

Date : 5-12-2025
Time: 8:00pm - 8:30pm 

## iNITIAL problem
--lsblk showed only vda (main OS disk)
--No practice disks present
 
 ## Solution
-- Shutdown RHEL VM
-- Added 3 * 5GB virtual disks via virt-manager
-- Restarted VM
-- Verified disks present:vdb,vdc,vdd

 ## Verification Test
```bash
 pvcreate /dev/vdb #SUCCESS
 pvs               #vdb listed 
 pvremove /dev/vdb #Cleanup

 ## Enviroment Status
--KVM: Running
--RHEL VM: Boots successfully
--Practice disks: vdb(5GB),vdc(5GB),vdd(5GB)
--LVM tools: Available
--Quick test: PASSED

 ## READY FOR TOMMOROW 
    Tommorow afternoon(2:30pm): FULL RAID 5 BUILD FROM DOCUMENT 2

 ## Transformation Evidence 
-- Tired + busy day, but showed up for 30 minutes
-- Encountered issue (no disks), solved it (added disks)
-- Verified enviroment functional
-- Tommorow unblocked and ready
