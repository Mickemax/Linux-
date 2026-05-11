# Storage basics
    - Hard disk drives are physical devices that store data using a set of desk platers that spin around, storing data magnetically on the platters with a movable read/write head that writes and retrieves magnetic images on the platters.
    - Solid-state drive use integrated circuits to store data electronically.

    # Drive Connections
    - Although HDDs and SSDs differ in how they store data, they both interface with the Linux system using the same methods.
        - Parallel Advanced Technology Attachment(PATA) connects drives using a parallel interface, which requires a wide cable. PATA suports two devices per adapter.
        - Serial Advanced Technology Attachment ( SATA) connects drives using a serial interface, but at a much faster speed than PATA. SATA supports up to four devices per adapter.
        - Small Computer System Interface (SCSI) connects drives using a parallel interface, but with the speed of SATA. SCSI supports up to eight devices per adapter.
        - Non-Volatile Memory Express(NVMe) connects solid-state drives using a parallel interface for maximum data transfer speeds. The NVMe standard supports up to 12 devices per adapter.
    - When you connect a drive to a Linux system, the Linux kernel assigns the drive device a file in the /dev folder. That file is called raw device, as it provides a path directly to the drive from the Linux system.
    - For PATA devices, the file is named /dev/hdx, where x is a letter representing the individual drive, starting with a. For SATA and SCSI devices, Linux uses /dev/sdx, where x is a letter representing the individual drive, again starting with a. With NVMe devices, Linux uses /dev/nvmex, again where x is a letter representing the individual drive.
    - Thus, to reference the first SATA device on the system, you'd use /dev/sda, and so on.

    # Partitioning Drives
        - A partition is a self-contained section within the drive that the operating system treat as a separate storage space.
        - Partitions must be tracked by some type of indexing system on the drive. 
            * BIOS boot loader uses MBR method and support 4 primary partitions on a drive, each partition itself, however, can be split into multiple extended partitions.
            * UEFI boot loader ses the more advanced GUID Partition Table (GPT) which support 128 partitions on drive.
        - Linux create /dev files for each separate disk partition.

    # Automatic Drive Detection
        - Linux systems detect drives and partitions at boot time and assign each one a unique device filename, but with the invention of removable USB drives it had to be modified.
        - Most Linux systems now use the udev application. The udev program runs in the background at all times and automatically detects new hardware connected to the running Linux system.
        - udev application also create persistent device files for storage devices, the /dev name assigned to it may change, depending on what devices are connected making it difficult for apps to find the same storage device each time to solve that problem udev uses the /dev/disk folder to create links to the /dev storage device files bsaed on unique attributes of the drive. 4 folders are creates for links.
            * /dev/disk/by-id links storage devices by their manufacturer make, model, and serial number.
            * /dev/disk/by-label links storage devices by the label assigned to them.
            * /dev/disk/by-path links storage devices by the physical hardware port they are connected to.
            * /dev/disk/by-uuid links storage devices by the 128-bit universally unique indentifier (UUID) assigned to the device.

# Partitioning Tools
    # Working with fdisk
        - The fdisk program allows you to create, view, delete and modify partitions on any drive that uses the MBR method of indexing partitions.
        - To use fdisk you must specify the drive device name.
        - It is rudimentary in that it doesn't allow you to alter the size of an existing partition; all you can do is delete the existing partition and rebuild it from scratch.

    # Working with gdisk
        - If you're working with drives that use the GPT indexing method, you'll need to use the gdsik program.
        - gdisk offers option to convert formatting your drive to a GPT drive.
    
    # The GNU parted command
        - The GNU 'parted' program provide yet another command-line interface for working with drive partitions.
        - One of the selling features of the parted program is that it allows you to modify existing partition sizes, so you can easily shrink or grow partitions on the drive.
            * The GNU parted package also contains the partprobe utility, which triggers the Linux system to reread the partition table for a specific disk.
    
    # Graphical Tools
        - GNOME Partition Editor, called GParted is a graphical tools available to use.
        - The gparted window display each of the drives on a system one at a time, showing all the partitions contained in teh drive in a graphical layout.
    
# Understanding Filesystems
    - filesystem is used to  manage data stored on a storage devices. A filesystem utilizes a method of maintaining a map to locate each file placed in the storage device.
    - Linux uses virtual directory structure that contains file paths from all the storage devices installed on the system consolidated into a single directory structure.

    # The Virtual Directory
         - It contains a single base directory, called the root directory.
         - Linux places physical devices in the virtual directory using mount points which is a folder placeholder within the virtual directory that points to a specific physical device.
         - The Linux Filesystem Hierarchy Standard(FHS) defines core folder names and locations that should be present on every Linux system and what type of data they should contain.
    
    # Maneuvering Around the Filesystem
        - Absolute path to a file always starts at the root folder(/) and includes every folder along the virtual directory tree to the file.
        - Relative path to a file denotes the location of a file relatice to your current location within the virtual directory tree structure.
        - If Linux sees the path is not starting with a forward slash it assume the path to be relative.

# Formatting Filesystems
    # Common Filesystem Types
        
        # Linux Filesystems
            - When you create a filesystem specifically for use on a Linux system there are seven main filesystems that you can choose from:
                * btrfs: It support up to 16 exbibyres (EiB) in size and a total filesystem size of 16 EiB.
                * eCryptfs: The Enterprise Cryptographic File System(eCrpyfs) applies a POSIX-compliant encryption protocol to data before storing it on the device.
                * ext3(ext3fs): It is a descendant of the original Linux ext filesystem. It supports files up to 2 tebibytes(TiB), with filesystem size of 16TiB.
                * ext4 : support files up to 16TiB with a tital of 1 EiB.
                * XFS: supports filesystems up to 8 exbibytes.
                * tmpfs: The temporary filesystem, it allows you to create a filesystem in memory that is destroyed when the system reboots.
                * swap: Create virtual memory for your system using space on a physical drive.
                    - ext4 and XFS both uses journaling which is a method of tracking data not yet written to the drive on a log file, called the journal.
        
        # Non-Linux Filesystems
            - Linux can handles non-linux filesystems; 
                * CIFS(Common Internet File System), HFS(Hierarchical File System), ISO-9660, NFS(Network File System), NTFS(New Technology File System), SMB(Server Message Block), UDI(Universal Disc Format), VFAT(Virtual File Allocation Table), ZFS(Zettabyte File System)

    # Creating Filesystems
        - mkfs program is actually a front end to several individual tools for creating specific filesystems.
    
    # Mounting Filesystems
        
        # Manually Mounting Devices
            - To temporarily mount a filesystem to the Linux virtual directory, use the mount command.
            - To remove a mounted drive from the virtual directory, use the umount command.
        
        # Automatically Mounting Devices
            - Linux maintains the /etc/fstab file to indicate which drive devices should be mounted to the virtual directory at boot time.
            - The first partition is mounted at the /boot/efi mount point in the virtual directory. The second partition is mounted at the root of the virtual directory and the third partition is mounted as a swap area for virutal memory.
            - A more dynamic method for automatically mounting filesystems is the autofs program.
        
 # Managing Filesystems

            # Retrieving Filesystem Stats
                - df displays disk usage by partition.
                - du displays disk usage by directory, good for finding users or applications ghat are taking up the most disk space.
                - fio display performance testing statistics from input/output tests on a filesystem.
                - iostat displays a real-time chart of disk statistics by partition.
                - lsblk displays current partition sizes and mount points.

            # Filesystem Tools
                - Linux uses the e2fsprogs package of tools to provide utilities for working with ext filesystems ( such as ext3 and ext4). The most popular tools in the efsprogs package are as follows:
                    - blkid displays information about block devices, such as storage drives.
                    - chattr changes file attributes on the filesystem.
                    - debugfs manually views and modifies the filesystem structure, such as undeleting a file or extracing a corrupt file.
                    - dump2fs displays block and superblock group information.
                    - e2label changes the label on the filesystem.
                    - resize2fs expands or shrinks a filesystem.
                    - tune2fs modifies filesystem parameters
                - These tools help you fine-tune parameters on an ext filesystem, but if corruption occurs on the filesystem, you'll need the fsck program.
                - The XFS filesystem also has a set of tools available for tuning the filesystem.
                    - xfs_admin displays or changes filesystem parameters such as the label UUID assigned.
                    - xfs_info, xfs_growfs, xfs_repair
                - If you are using btrfs filesystem, the btrfs command provides access to several utilities for managing the filesystem:
                    - balance, check, device, filesystem, quota, restore.

# Storage Alternatives
    
    # Multipath
        - The Linux kernel now supports Device Mapper Multipathing(DM-multipathing), which allows you to configure multiple paths between the Linux system and network storage devices.
            * dm-multipath, multipath,multipathd, kpartx
        - The DM-multipath features uses the dynamic /dev/mapper device file folder in Linux.
    
    # Logical Volume Manager
        - The LVM also utilizes the /dev/mapper dynamic device folder to allow you to create virtual drive devices.
        - The benefit of LVM is that you can add and remove physical partitions as needed to a logical volume, expanding and shrinking the logical volume as needed.
        - If you run out of space in a logical volume, just add a new disk partition to the volume.
    
    # Using RAID Technology
        - Redundant Array of Inexpensive Disk technology has changed the data storage environment for most datacenters.
        - RAID allows you to improve data access performance and reliability as well as implement data redundancy for fault tolerance by combining multiple drive into one virtual drive.
            There are few several version:     
                * RAID-[0,1,10,4,5,6]
        - The mdadm utility allows you to specify multiple partitions to be used in any type of RAID environment.
    
    # Encrypting Partitions
        - Encrypting the entire partition where the data can be stored. A popular tool for that is the Linux Unified Key Setup (LUKS).
        - The core utility in LUKS is the cryptsetup utility. It allows you to create encrypted partitions, then open them to make them available for formatting and mounting in the Linux virtual directory.

