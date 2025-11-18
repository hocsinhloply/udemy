# Request Amazon EBS volume modifications

- Request Amazon EBS volume modifications: https://docs.aws.amazon.com/ebs/latest/userguide/requesting-ebs-volume-modifications.html
- You can check the file system size to see if your instance recognizes the larger volume space. On Linux, use the df -h command to check the file system size.
- Extend the file system after resizing an Amazon EBS volume: https://docs.aws.amazon.com/ebs/latest/userguide/recognize-expanded-volume-linux.html
- Check whether the volume has a partition. Use the lsblk command: sudo lsblk
- Check whether the partition needs to be extended. In the lsblk command output from the previous step, compare the partition size and the volume size.
- Extend the partition. Use the growpart command and specify the device name and the partition number:
- The partition number is the number after the p. For example, for nvme0n1p1, the partition number is 1. For nvme0n1p128, the partition number is 128.
- To extend a partition named nvme0n1p1, use the following command: sudo growpart /dev/nvme0n1 1
- Verify that the partition has been extended. Use the lsblk command. The partition size should now be equal to the volume size.
- Extend the file system.
- Get the name, size, type, and mount point for the file system that you need to extend. Use the df -hT or lsblk -f command.
- The commands to extend the file system differ depending on the file system type. Choose the following correct command based on the file system type that you noted in the previous step. 
- [XFS file system] Use the xfs_growfs command and specify the mount point of the file system that you noted in the previous step: sudo xfs_growfs -d /
- [Ext4 file system] Use the resize2fs command and specify the name of the file system that you noted in the previous step: sudo resize2fs /dev/nvme0n1p1
- Make an Amazon EBS volume available for use: https://docs.aws.amazon.com/ebs/latest/userguide/ebs-using-volumes.html#ebs-format-mount-volume
- Format and mount an attached volume
- Use the lsblk command to view your available disk devices and their mount points (if applicable) to help you determine the correct device name to use.
- The output of lsblk removes the /dev/ prefix from full device paths.
- Determine whether there is a file system on the volume:
  - Use the file -s command to get information about a specific device:  If the output shows simply data, there is no file system on the device
  - If the device has a file system, the command shows information about the file system type.
- Use the lsblk -f command to get information about all of the devices attached to the instance: sudo lsblk -f
- Use the blkid command to find the UUID of the device

Make an Amazon EBS volume available for use: https://docs.aws.amazon.com/ebs/latest/userguide/ebs-using-volumes.html#ebs-format-mount-volume
Use the blkid command to find the UUID of the device

df -hT /: check file system type, df disk free hiển thị thông tin file system, -h human read, -T hiển thị loại, -t <type> hiển thị loại filesystem chỉ định, -i hiển thị thông tin dung lượng inode
Resize partition then resize file system
sudo resize2fs /dev/root (với kiểu ext4 dùng resize2fs, /dev/root là file system)

## Extend current EBS volume
- Modify current volume
- Check the volume is modified: sudo lsblk -f
- Extend partition or create new partition:
  - Extend: Example sudo growpart /dev/nvme0n1 1
  - Create new partition => format partition (follow below direction)

## Mount new EBS volume
1. Create the new EBS volume
2. Attach volume in Console (EBS volume have to create in the same AZ with instance)
3. Check if this volume available = lsblk
4. Check device has a file system? = sudo file -s {device name} or use sudo lsblk -f
- Ex Result: /dev/xvdf: data => no file system
- Ex Result: dev/xvda1: SGI XFS filesystem data (blksz 4096, inosz 512, v2 dirs) => has

(Optional)
- Seperate partitions: 
  - sudo parted /dev/nvme1n1
  - mklabel gpt (Create Partition Table has type gpt)
  - mkpart primary ext4 0% 5GB (ext4 o day chi la label => chua co filesystem)
  - mkpart primary ext4 5GB 100%

5. Create file system: mkfs -t command to create a file system on the volume.
- sudo mkfs -t xfs /dev/nvme1n1 (xfs)
- sudo mkfs –t ext4 /dev/nvme1n1 (ext4)
6. Create a mount point directory for the volume: sudo mkdir /data
7. Mount volume at the mount point directory:  sudo mount /dev/xvdf1 /data

**Automatically mount an attached volume after reboot**

- Remove file system: sudo wipefs -a /dev/nvme1n1
- File system là cấu trúc logic bên trong partition => cách chia block, lưu inode, ghi dữ liệu, quản lý tên file, quyền, ....
- Seperate partitions: 
  - sudo parted /dev/nvme1n1
  - mklabel gpt (Create Partition Table has type gpt)
  - mkpart primary ext4 0% 5GB (ext4 o day chi la label => chua co filesystem)
  - mkpart primary ext4 5GB 100%

## Inode
- Inode stands for Index Node
- Inodes **stores metadata** for every file on your system in a table-like structure usually located near the beginning of a partition.
- They store all the information **except the file name and the data**.
- Inodes stores metadata about the file it refers to. This metadata contains all the information about the said file.
  - Size
  - Permission
  - Owner/Group
  - Location of the hard drive
  - Date/time
  - Other information
- Every used inode refers to 1 file. Every file has 1 inode. Directories, character files, and block devices are all files. They each have 1 inode.
- For each file in a directory, there is an entry containing the filename and the inode number associated with it.
- Inodes are **unique at the partition level**. You can have two files with the same inode number given they are on different partitions.
- List the inodes number = `ls -i`
- List inode information for each file system = `df -hi`
- Soft/ Hard link
  - When you create a **soft link**, you create a **new file**. In its metadata, it points to the target. For every soft link you create, you use one inode.
  - A **hard link** does **not create a new file**. It only provides a new name for the same data. Because a hard link has the same inode number as the original file, you can delete the original file and the data is still available through the hard link.
  - Inodes are also a big reason why a Linux system can update without the need to reboot. This is because one process can use a library file while another process replaces that file with a new version. Therefore, creating a new inode for the new file. The already running process will keep using the old file while every new call to it will result in using the new version.
