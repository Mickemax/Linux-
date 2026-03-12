# The Linux Boot Process

    # Following the Boot Process
        - The workstation firmware starts, performing a quick check of the hardware( called Power-On Self Test - POST )and then looks for a bootloader program to run from a bootable device.
        - The bootloader runs and determines what Linux Kernel program to load.
        - The Kernel program loads into memory and starts the necessary background programs for the system to operate( such as a graphical desktop manager for desktops orweb datbase servers fro servers).
    
    # Viewing the Boot Process
        - You can monitor the Linux boot process by watching the system console screen as the system boots. You'll see lots of informative messages scroll by as the systyem detects hardware and loads software.
            * Some graphical desktop linux distribution runs the boots on a seperate console. "CTRL+ALT+F1 key" to view those message.
            * If you need to troubleshoot boot problems, you can review the boot time messages using the dmesg command.
            * Most linux distributions also store the boot messages in a log file, usually in the /var/log folder.
                    For both Debian and Red Hat-based systems, the file is usually /var/log/boot.log, but some legacy systems may use /var/log/boot.
            
            # The FirmWare Startup
                On older computer it is called the BIOS( Basic Input Output System), on newer ones UEFI( Unified Extensible Firmware Interface),maintain the system hardware status and launched an install OS.
                    
                    - The BIOS startup
                        One limitation of the BIOS is it could read only one sector's worth of data from a hard drive into a memory to run.
                        Most OS( linux and Window), split the process into two parts.
                            * BIOS runs a bootloader program, a small program that initialize the necessary hardware to find and run the full OS program. It usually has a configuration file, so you ca tell it where to find the actual OS file.
                                - First the BIOS needs to know where to find the bootloader program on an installed storage device.
                                        * Internal HD, External HD, A CD or DVD drive, A USB memory stick, An ISO file, A network server using FTP, NFS, HTTP.
                                - When booting from HD, you must designate the hard drive, and the partition on the hard drive, from which the BIOS should load the bootloader program. By defining a Master Boot Record(MBR).
                    
                    - UEFI Startup
                        UEFI specifies a special disk partition, called the EFI System Partition (ESP), to store bootloader programs to store bootloader programs.
                            The ESP setup utilizes the old Microsoft File Allocation Table(FAT) filesystem to store the bootloader programs.
                            On Linux systems, the ESP is typically mounted in the /boot/efi.
                        With UEFI, you need to register each individual bootloader file you want to appear at boot time in the boot manager interface menu(built-in mini-bootloader).
            
            # Linux Bootloaders
                The bootloader program helps bridge thegap between the system firmware and the full Linux operating system kernel.
                    Bootloader program that have been used by default;
                      - Linux Loader(LILO)
                            LILO was very limited,loading the Linux kernel from the BIOS startup. its configuration file is stored in a single file, /etc/lilo.conf. It is not UEFI compatible.
                      - Grand Unified Bootloader (GRUB) Legacy
                            It was a more robust version of the LILO, GRUB quickly became the default bootloader for all linux distributions, whether they were run on BIOS or UEFI systems.
                      - GRUB2
                            It supports advanced features, such as the ability to load hardware driver modules and using logic statements to dynamically alter the boot menu options.
            
            # GRUB Legacy
                - The GRUB legacy bootloader was designed to simplify the process of creating boot menus and passing options to kernels.
                - Allows you to select multiple kernels and/or operating systems using both a menu interface and an interactive shell.
                    * you configure the menu interface to provide options for each kernel or OS you want to boot with.
                    * Interactive shell provides a way for you to customize boot commands on the fly.
                
                # Configuring GRUB Legacy
                    - You need to tell what options to show using special GRUB menu commands.
                    - It stores the menu commands in a standard text configuration file, called "menu.lst"(Red-hat uses grub.conf). The file is store in /boot/grub folder.
                        * The grub legacy configuration file consists of two sections:
                            
                            - Global definitions
                                It defines commands that control the overall operation of the GRUB Legacy boot menu. It must appear first in the configuration file.
                                    * For GRUB Legacy, to define a value for a command you list the value as a command-line parameter:
                                        - color command: Defines the color scheme for the menu. the first and second pair defines the foreground/background pair for normal menu and selected menu respectively.
                                            There are a lot of boot definition settings that you can use to customize how the bootloader finds the operating system kernel file.Only a few are required to define the OS.
                                                - Title: the first line for each boot definition section; appears in the boot menu.
                                                - Root: Defines the disk and partition where the GRUB/root folder partition is on the system.
                                                - Kernel: Defines the kernel image file stored in the /boot folder to load.
                                                - Initrd: Defines the initial RAM disk file, which contains drivers necessary for the kernel to interact with the system hardware.
                                                - Rootnoverify: Defines non-linux boot partitions, such as Windows.
                                        
                                        - root command:  defines the hard drive and partition that contains the /boot folder for GRUB Legacy.
                                            ( hddrive, partition) - (hd0,0) first partition on first hard drive.
                                        
                                        - initrd command: It helps solve a problem that arises when using specialized hardware or filesystems as the root drive.
                                            * It defines a file that's mounted by the kernel at boot time as a RAM disk. The kernel can then load modules from the initrd RAM disk, which allows it to access hardware  
                                                or filesystems not compiled into the kernel itself. /boot directory. called initrd.img-kversion, where kversion is the kernel version number.
                                            * If you install new hardware on your system that's required to be visible at boot time, you will need to modify the initrd file. 
                                                    - mkinitrd command in Red Hat-based system.
                                                    - mkinitramfs in Debian-based systems.
                                            
                    # Installing GRUB Legacy
                        - Install the grub legacy in the MBR.
                            grub-install
                        - uses a single parameter- either specify the partition using Linux or GRUB legacy format.
                            Linux: grub-install /dev/sda
                            GRUB: grub-install '(hda)'
                        -If using chainloading method and prefer to install a copy of GRUB legacy on the boot sector of a partition instead of to the MBR of a hard drive.
                            grub-install /dev/sda1
                            grub-install 'hd(0,0)'

            # GRUB2
                The configuration file name is 'grub.cfg' and stores it in the /boot/grub/ folder. Some Red Hat-based Linux distributions also make a symbolic link to this file in the /etc/grub2.cfg file for easy reference.

                # configuring GRUB2
                    - Uses meneuntry command instead of the title command, and you must enclose each individual boot section with braces immediately.
                            menuentry "Ubuntu Linux" {
                                set root=(hd1,1)
                                linux /boot/vmlinuz
                                initrd /initrd
                            }   

                            menuentry"Windows" {
                                set root=(hd0,1)
                            }   

                    - Uses the set command to assign value to the root keyword and an equal sign to assign the device.
                        * Change partition numeration starting with 1, and hard drive to 0.
                    - rootnoverity and kernel are not used, non-Lunix boot options are now defined the same as Linux boot options using the root environment variable.
                    - You define the Kernel using Linux command.
                    - /boot/grub/grub.cfg file is the configuration file and should not be modified.
                    - /etc/grub folder. This allows you to create individual config file for each bot option installed on your system( Linux and Windows).
                    - /etc/default/grub configuration file for global commands.

                # Installing GRUB2
                    You rebuild the main installation file by running the 
                        grub2-mkconfig program which reads configuration files stored in the /etc/grub.d folder.
                    You can update the configuration file manually by running; # grub2-mkconfig -o /boot/grub2/grub.cfg  
                            -o redirect output to the file.

                    Situations where you need to reinstall the grub2, after creating grub.cfg configuration file you can install it onto the primary hard disk using the 'grub2-install' command:
                        # grub2-install /dev/sda
                    
                    # update-grub2

            # Alternative Bootloaders
                - SYSLINUX: A bootloader for systems that use the Microsoft FAT filesystem.
                - EXTLINUX: A mini-bootloader for booting from an ext2, ext3, ext4, or btrfs filesystem.
                - ISOLINUX: A bootloader for booting from a LiveCD or LiveDVD. Requires iso.linux.bin which contains the bootloader program image and isolinux.cfg which contains teh configuration settings.
                - PXELINUX: A bootloader for booting from a network server. uses Pre-boot eXecution Environment standard, which defines how a network workstation can boot and load an OS from a centreal network server.
                - MEMDISK: A utility to boot older DOS OS from the other SYSLINUX bootloaders.


    # System Recovery
        - Kernel Failures
            When the Linux kernel stops running in memory, it is referred to as a kernel panic. It is often due to installing a new kernel without the appropriate module or library changes or starting a program at a new runlevel.
                # selecting Previous Kernels at Boot
                    When you install a new kernel file, it's always a good idea to leave the old kernel file in place and create an additonal entry in the GRUB boot menu to poin to the new kernel.

                        # Single-User Mode
                            At times you may need to perform some type of system maintenancem such as add a new hardware module or library file to get the system to boot properly.  
                                - GRUB menu allow you to start in single user mode by adding 'single' command. To get there press E key on the boot option.
                        
                        # Passing Kernel Parameters
                            Here, you can add other kernel parameters to the linux command in the GRUB boot menu,which alter the hardware modules it activates.
                    
        - Root Drive Failure
            # Using a Rescue Disk
                The rescue disk usually boots either from the CD drive or as a USB stick and loads a small Linux system into memory.
                     # fsck command
                        checking and fixing hard drive errors. fsck is an alias for a family of commands specific to different types of filesystem(ext2, ext3 and ext4) You need to run the command against the device name if the partition that contains the root directory of your Linux system.
                            # fsck /dev/sda1
                     Attempt to reconcile the inode tablle and file blocks stored on the hard drive.
                            # Rocky uses xfs and instead use the xfs_repair tool, for fsck won't work as it's intended for te ext filesystems.
                                'df -Th' to list the partitions and their filesystem types.
            
            # Mounting a Root Drive
                When the fsck (or xfs_repair) repair is complete, you can test the repaired partition by mounting it into the virtual directory created in memory.
                    # mount /dev/sda1 /media
                
                You can examine the filesystem stored in the partition to ensure that it's not corrupted. Before rebooting, you should unmount the partition.
                    #umount /dev/sda1





                    
                    A
                    B
                    D
                    C
                    ABCDE
                    ABE
                    D
                    E
                    B
                    A
                    BC
                    C
                    A
                    B
                    D
                    A
                    A
                    D
                    C
                    A

                

                    






                                        
                            

                                        
            


            