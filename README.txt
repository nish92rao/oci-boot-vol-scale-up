!!!DO NOT DEMO THIS ON PRODUCTION!!!

Oracle Linux 8 & 7:
1. df -h: 36GB for /dev/mapper/ocivolume-root
	lsblk: 46.6GB for /dev/sda
2. Increase boot volume size (to 60GB). Rescan commands:
sudo dd iflag=direct if=/dev/oracleoci/oraclevda of=/dev/null count=1
echo "1" | sudo tee /sys/class/block/`readlink /dev/oracleoci/oraclevda | cut -d'/' -f 2`/device/rescan
3. lsblk: 57G for /dev/sda
4. sudo /usr/libexec/oci-growfs -y
5. df -h

Oracle Linux 6:
1. df -h: 36GB for /dev/mapper/ocivolume-root
	lsblk: 46.6GB for /dev/sda
2. Increase boot volume size (to 60GB). Rescan commands:
sudo dd iflag=direct if=/dev/oracleoci/oraclevda of=/dev/null count=1
echo "1" | sudo tee /sys/class/block/`readlink /dev/oracleoci/oraclevda | cut -d'/' -f 2`/device/rescan
3. sudo growpart /dev/sda 3
4. Reboot instance


CentOS 8 increase Boot volume size:

1. df -h : 40GB for /dev/mapper/centosvolume-root
2. sudo fdisk -l : 
3. Increase boot volume size (to 60GB) and reboot. Rescan commands:
sudo dd iflag=direct if=/dev/oracleoci/oraclevda of=/dev/null count=1
echo "1" | sudo tee /sys/class/block/`readlink /dev/oracleoci/oraclevda | cut -d'/' -f 2`/device/rescan
4. sudo fdisk -l
5. sudo fdisk /dev/sda
i. n -> Enter -> Enter -> Enter
ii. t -> Enter -> 31
iii. p
iv. w
6. sudo pvcreate /dev/sda4
7. sudo vgdisplay
8. sudo vgextend centosvolume /dev/sda4
9. sudo lvdisplay
10. sudo lvextend -l +100%FREE /dev/centosvolume/root
11. sudo xfs_growfs /dev/mapper/centosvolume-root
12. df -h

Other method for CentOS 8:

1. df -h: 40GB for /dev/mapper/centosvolume-root
2. Increase boot volume size (to 60GB) and reboot. Rescan commands:
sudo dd iflag=direct if=/dev/oracleoci/oraclevda of=/dev/null count=1
echo "1" | sudo tee /sys/class/block/`readlink /dev/oracleoci/oraclevda | cut -d'/' -f 2`/device/rescan
3. sudo growpart /dev/sda 3
4. lsblk -b (copy the size of /dev/sda3)
5. sudo pvresize --setphysicalvolumesize <size> /dev/sda3
6. sudo lvdisplay
7. sudo lvextend -l +100%FREE /dev/centosvolume/root
8. sudo xfs_growfs /dev/mapper/centosvolume-root
9. df -h

CentOS 7:
1. df -h: 39GB for /dev/sda3
2. Increase boot volume size (to 60GB) and reboot. Rescan commands:
sudo dd iflag=direct if=/dev/oracleoci/oraclevda of=/dev/null count=1
echo "1" | sudo tee /sys/class/block/`readlink /dev/oracleoci/oraclevda | cut -d'/' -f 2`/device/rescan
3. sudo yum install gdisk -y
4. sudo growpart /dev/sda 3
5. sudo xfs_growfs /dev/sda3
6. df -h


Windows:
1. Increase boot volume size (to 60GB).
2. Start > Search 'Disk Management' and open
3. Right-click C: drive > Extend Volume
4. Click Next & Next & Finish


Ubuntu:
1. Increase boot volume size (to 60GB).
2. Reboot instance