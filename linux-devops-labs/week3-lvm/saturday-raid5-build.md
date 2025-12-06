## Saturday RAID 5 Build - Complete

Date: 6-12-2025
Time: 7:00pm - 9:00pm
Duration : 2 hours

## What I Built 
  RAID 5 LVM on KVM/RHEL enviroment:
-- 3 physical disks: vdb,vdc,vdd (5GB each)
-- Volume Group: VolGroup1 (~15GB)
-- Logical Volume : lv1 (RAID 5 type)
-- Filesystem: XFS
-- Mount point: /space (~10GB usable)

## Command Sequence 
 
 # Physical Volumes 
 pvcreate /dev/vdb /dev/vdc /dev/vdd 

# Volume Group
vgcreate VolGroup1 /dev/vdb /dev/vdc /dev/vdd

#  RAID 5 logical Volume
lvcreate -l +100%FREE --type raid5 -n lv1 VolGroup1

# Format and Mount 
mkfs.xfs /dev/mapper/VolGroup1-lv1
mkdir /space
mount /dev/mapper/VolGroup1-lv1 /space

# Verification

df -h | grep space 
LVM PRACTICE

Start the machine -- RHEL 9
log in : username and password
become root -- sudo su -
verify block devices -- lsblk
*output* : vdb,vdc,vdd listed 
pvcreate /dev/vdb, reapeated for /dev/vdc and vdd
output .../dev/vdd" successfully created 
pvs 
*output* list /dev/vda2 psize <24.00g pfree 0 
and /dev/vdb.../dev/vdd lvm2 psize 5.00g, Pfree 5.00g
pvdisplay show more info...NB: very important to know what is usable 
vgcreate VolGroup1 /dev/vdb /dev/vdc /dev/vdd
--- volume group "VolGroup1" successfully created 
vgs 
--- volgroup1 pv=3,lv=0 vsize =14.99g vfree=<14.99, then rhel pv 1, lv =2 Vsize <24.00g vfree=0
verify with vgdispaly volgroup1 
-- list detaioled info..  questions{w hat is the PE  size in the output mean}
Raid 5 logical volume 
lvcreate =l +100%FREE  --type raid5 lv1 VolGroup1
--Logical Volume "lv1" created 
lvs
-- volgroup1 present Lsize 9.98g cpy%sync 100.00
lvs -a --- more info
check raid status 
lvs -a -o +devices ;
-- shows more info and the physical devices being used 
format with XFS
mkfs.xfs /dev/mapper/volgroup1-lv1
--block size , sector info ...
mount 
mkdir /space
mount manually (don't use fstab--can crash system)
mount /dev/mapper/volgroup1-lv1 /space
verify 
df -h | grep space 
--show :  /dev/mapper/VolGroup1-lv1 10G 9.98 2% /space(10G is ~66% of 15G due to RAID 5 parity)
mount | grep space 
--shows type xfs
lvs 
-- shows: VolGroup1 present L size 9.98G cpy%sync 100.00
mount | grep /space
-- shows type xfs

## Undersatnding Check

*** RAID 5 Characteristics:**
-- Minimum disks: 3 
-- Usable capacity: ~66% (parity uses on disk equivalent)
-- Redundancy: Can lose 1 disk without data loss 
-- My setup: 15GB raw == 10GB usable 

** Time taken to Complete:**
-- First attempt(setup + build ): 1 hr
-- Could now rebuild in : ~20 minutes from memory

*** Confidence Level
-- Understand RAID 5 concept: YES
-- Can build from memory:MOSTLY(may need to reference some flags)
-- Ready to move Forward: YES

## Key Learnings 

-- RAID 5 initialization takes time (1-2 minutes for lvcreate)
-- Manual mount safer than fstab for practice 
-- XFS formatting faster than ext4
-- lvs -a show RAID metadata volumes
-- Second build faster than first

## Next Steps 
-- Teardown this build 
-- Move to week 4 systemd practice 
-- Unit 3 complete, ready for Week4 content
