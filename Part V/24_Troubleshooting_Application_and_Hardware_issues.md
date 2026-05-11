# Dealing with Storage Problems
    - Troubleshooting storage issues ranges from the easy-to-check items all the way to the strange and obscure.

    # Exploring Common Issues
        - Most likely unaware common storage problems.
            # Degraded Storage/Mode:
                - Degraded storage refers to the storage medium's gradual decay due to time or improper use, which causes data degeneration or loss.
                - Degraded mode refers to a situation in which one or more disks in a RAID array have failed. In this case, troubleshooting efforts require you to employ the mdadm -D command to view a particular array's detailed status.

            # Missing Devices
                - Storage devices can go "missing" on Linux, but the cause varies. If it is network attached storage (NAS), check your network first.
                - If it is locally attached device and other utilities, such as lsblk, are not displaying it, use super user privileges and try the lspci -M command. This will perform a thorough scan of all PCI attached devices.
            
            # Missign Volumes
                - Another form of a lost device is a missing volume. If you perform a pvscan on the physical devices that make up a logical volume and get a "Couldn't find device" message, you've got a missing volume.
                - Typically, the cause is a failed or unintentionallt removed disk. If a disk that was of a logical volume's group has failed, the missing disk's UUID will display in the pvscan message.
            
            # Missing Mount Points
                - A "Mount point does not exist" error message implies the obvious - the directory on which you are attempting to mount the filesystem does not exist.
                - However, this error message can also be generated for a not-so-obvious problem. It centers on employing the bind option, either at the command line via the mount command or the bind option, either at the command line via the mount command or the /etc/fstab file.
            
            # Storage Integrity
                - A bad block( also called a bad sector) is a small chunk of a disk drive that will not respond to I/O requests due to corruption or physical damage.
                - A random bad block does not indicate a drive is failing, but these storage devices need monitoring, because increasing bad sectors indicate it needs replacing.
                - Beside using the fsck command, you can use the badlocks utility to monitor a drive, which focus on a particular partition and does not perform any repairs.
                - It is wise to unmount a partition prior to checking for bad sectors.
            
            # Performance Issues
                - Poor storage performance adversely affects applications. Beside using utilities such as iostat, ioping, iotop and sar to monitor storage performance problems, you can also employ hdparm to determine a drive's read speeds.
                - This utility is useful for PATA or SATA drives. SCSI drives that have SCSI/ATA command translation are also supported.
                - The dstat utility is similar to iostat but provides additional helpful data for troubleshooting storage performance problems.
                - Another handy utility that works specifically with logical volumes is the dmstats utility.
                - This tool allows the setup and management of statistics for any devices charted by the device mapper.
            
            # Resource Exhaustion 
                - Resource exhaustion is situation in which a system's finite resources are committed and unavailable to others.
                - Running out of inode numbers or disk space are two examples.
    
    # Dealing with Specialized Issues
        - One of the first things you should check for an older storage device experiencing problems is whether the device's manufacturer has a new driver or firmware available.
        - Another item to check is the device's Linux module (driver). If it is not loaded or built into the Linux kernel, yur device will not function.
        - Start with the dmesg utility to gain some clues. The dmesg utility's output is searched using grep to find information concerning the sde disk(/dev/sde). The disk is an attached SCSI disk.
        - The available SCSI driver information is stored within a /sys/ directory.
        - If the module is not loaded, it may be built into the kernel. You can check this by looking at the modules.builtin file.
    
        # Seeking SATA
            - An Adapter is a piece of hardware that may have one or more software interfaces. The various storage interfaces, such as SATA drives, can have unique problems. 
            - On Linux, SATA drives are self-configuring. THey are typically connected to the SCSI bus and are denoted by the /dev/sd* device files.
            - Some SATA device may fail earlier due to frequent head loads and unloads. YOu can cheeck for this situation on a SATA drive, if it uses self-monitoring analysis and reporting technology ( SMART), via the smartctl -a command.
        
        # Comprehending SCSI
            - On Linux, the SCSI framework consists of three integral parts:
                * Upper: The device driver layer.
                * Middle: The SCSI routing layer.
                * Lower: The host bus adapter (HBA) driver layer.
            - The upper layer is closest to the application or user command, whereas the lower SCSI layer is right next to the actual hardware. THe HBA is either a circuit board or an integrated circuit adapter, which connects to the disk drive.
        
        # Moderating RAID
            - A Linux system can employ software and hardware RAID. Software RAID arrays are implemented through the Multiple Device (md) driver.
            - Check the status of your software RAID array by viewing the /proc/mdstat file.
            - If it is SATA based and a drive goes offline,  a software RAID array can hang. This occurs if the HBA does not handle hot-plugging action.
            - Hardware-based RAID arrays are managed via a hardware device connected to the Linux SCSI framework. A hardware RAID controller's data, such as the manufacturer and model number, is obtained using super using privileges and enterign lspci -knn | grep  " RAID bus controller" at the command line.

# Uncovering Application Permission Issues
        - A user notifies you that an application has issued an I/O error when they attemot to run it. the problem is possibly a permission issue. 
        - You will need to gather some information prior to starting your troubleshooting:
            * Determine which account runs the application and the account's name.
            * Discover the specific program action that raised the error.
            * Obtain a full directory reference for any files on which the application was attempting to perform reads/writes or for any files it was attempting to create.
            * Record, if applicable any additional applications it was trying to launch
            * Document, if applicable, any local or remote services the application is attempting to employ, such as NTP or a file server.
        - When you have these details, you are ready to proceed in your troubleshooting process.
            - Ownership: Look at the various application files involved using the ls -l command.
            - Group Memberships: Uncover the groups to which the end user running the application belongs.
            - Executables: If the application cannot be run by a particular account, check the execute privileges.
            - Inheritance: If the application is creating files in a particular directory and can no longer access those files, check for forced inheritance via ACLs.
    
# Analyzing Application Dependencies
    # Versioning
        - Typically, application software programs and operating systems are continually updated. These updates may improve performance or add additional functionality. To keep track of the various application updates, a technique called versioning is employed.
    
    # Updating Issues
        - If an application is experiencing problems, check for a new software update. If the application is available through a repository, use your distro's particular package management to check for a new verison.
    
    # Patching
        - A patch refers to program changes or configuration file updates for a particular application or system service. Patches may correct serious problems or fix security vulnerabilities and are often issued out of the normal software update cycle.
    
    # Dealing with Libraries
        - Application functions are often split into separate library files so that multiple applications that use the same functions can share these library files.
        - If an application begins experiencing problems after a software upgrade, it may be related to a recently upgraded shared library the application employs.
    
    # Exploring Environment Variable Issues
        - If you have a newly application that is not executing, check the PATH environment variable. This particular variable determines what directories are searched for a program that the Bash shell does not directly handle.
    
    # Gaining GCC Compatibility
        - The most common tool used for compiling programs in Linux is the GNU Compiler Collection (GCC). If you have problems compiling an application on Linux with GCC, there are several potential causes, They are as follows:
            * GCC uses the system C library, which might not be compliant with the ISO C standard.
            * There are several notable incompatibilities between GNU C and non-ISO version of C.
            * GCC uses corrected versions of system header files, which can cause issues.
    
    # Perusing Repository Problems
        - The very first thing to check when you get an old error message concerning a package that cannot be found, updated, or installed is your network connection.
        - Often a system that is not network-connected causes this problem.
        - Debian uses apt-get clean command, then apt-get update.
        - Red Hat package manager, such as Rocky Linux, you can employ the yum clean all or zypper clean -a command, depending on your distro.
        - If you are attempting to install or update packages from a nonstandard repositoru, you may need to enable that repo on your system.
    
# Looking at SELinux Context Violations
    - Application issues can be caused by your system's Linux kernel security module, such as SELinux.
    - An incorrect policy configuration, which triggers a violation, can prevent applications from serving their purpose.
    - Check the audit log file using the sealert command first. If this tool is not available you can install it via the setroubleshoot package.

# Exploring Firewall Blockages
    - If an application is experiencing problems over the network and there are no network issues, you may want to check the local and remote systems' firewalls.
      
        # Unrestricting ACLs
            - A firewall ACL identifies a network packet by reviewing its control information along with other network data.
            - Therefore, when troubleshooting an application issue related to a firewall, you'll need to gather the following information for the application packets traveling back and forth:
                * Source addrress or hostname
                * Destination address or hostname
                * Network protocol(s) used
                * Inbound port(s) used
                * Outbound port(s) used
        
        # Unblocking Ports
            - If your application relies on another system service ( daemon), you'll want to check rules related to the service port.
            - Blocking a paort needed by the external service would adversely affect the application is designed to use a port that is not dedicated to a well-known service, check it as well.
        
        # unblocking Protocols
            - Besides ports, be aware of the various protocols, such as UDP, TCP, and ICMP, that your application employs. If it uses another system service, you must know the protocols it uses as well.
            - The /etc/services file can help.
    
# Troubleshooting Additional Hardware Issues
    - Linux requires hardware to operate. When hardware stops working correctly, Linux does not function properly.

        # Looking at Helpful Hardware Commands
            - When you are troubleshooting hardware problems, there are many Linux command-line tools that can help. The lspci, lsusb, and lsdev commands are a few.

            # Understanding the dmidecode Utility 
                - DMTF created the Desktop Management Interface (DMI) and System Management BIOS standards. The DMI specification consists of four components, which  provide information about the hardware being used on a computer as well as some additional helpful data.
                - The help option on the dmidecode utility describes the various options you can use to uncover information in your hardware troubleshooting process. While you must use super user privileges with the command for extracting table information, you don't have to do so for getting help.
                - If the tables do not contain the needed information, you will only receive a message about where the utility attempted to extract data and possibly DMI and/or SMBIOS standard versions supported.
            
            # Understanding the Ishw Utility
                - hardware information is stored in various /proc/ directory files on your system. While you could go rooting around and dig it out yourself, the lshw utility does it for you.
                - It provides data on your system's processor(s), memory, NIC(s), USB controller(s), disk(s), and so on.
                - It is typically installed by default on most distributions or available in a standard repository.
                - The different classes available are displayed in the lshw -short command's output.
            
            # Investigating Other Hardware Problems
                - Occasionally you have a hardware problem that is uncommon. Being able to quickly address these unique issues will make you stand out from your peers.
                    # Memory
                        - Physical problems with RAM are tricky to diagnose. Some symptoms of this issue include a system's performance slows over time, the system appears to hang when a memory-intensive application is running or a boot, kernel panics or segmentation faults occur intermittently, files are sporadically corrupted, and/or program installations fail.
                        - First make sure it is not a memory capacity issue, which often shows symptioms similar to hardware problems.
                    
                    # Printers
                        - External hardware devices are typically plug and play for Linux, but odd problems do arise. When dealing with printers, the issue typically comes down to either an outdated/incorrect driver (PPd) or a bad connection.
                    
                    # Video 
                        - Hardware issues with video show up in sluggish displays, audio lag, glitches on the screen, and so on. You may even see a black screen or receive no audio output.
                        - Some problems can even cause the system to crash or hang.
                    
                    # Communications Ports
                        - A communications port is a serial communications port. Though a rarity nowadays, it is often used to connect hardware such as point-of-sale devices.
                        - The files that represent these serial ports are /dev/ttyS#
                    
                    # USB 
                        - If you have a USB device, such as a printer, directly attached to your system and problems occur, there are some simple troubleshooting techniques you can employ.
                        - First ensure that the USB module ( driver) is loaded into the kernel by using super user privileges and typing lsmod | grep usb at the command line.
                        - If the driver is already loaded, try detaching the device's USB cable from the system. Watch the journal file by issuing the journalctl -f command.

                    # Keyboard
                        - If you press a key on you keyboard and a different letter appears on the screen, most likely you have a keyboard mapping issue. The fix depends on the particular distribution you are using.
                        - For Red Hat-based distros, type localectl with no options and your current key map will display. To see the list of available key maps, enter localectl list-keymaps and a list of available key mappings will display.
                    
                    # Hardware or Software Compatibility Issues
                        - Before you purchase any new hardware, make sure it will work with yur Linux distribution. Keep in mind that while Linux is the number-one operating system kernel for super computers and a strong contender in the server world, it does not always get the attention it deserves from hardware manufacturers.