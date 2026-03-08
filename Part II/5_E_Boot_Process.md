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
                    - It stores the menu commands in a standard text configuration file, called "menu.lst"( Red-hat uses grub.conf). The file is store in /boot/grub folder.
                        * The grub legacy configuration file consists of two sections:
                            
                            - Global definitions
                                It defines commands that control the overall operation of the GRUB Legacy boot menu. It must appear first in the configuration file.
                                    * For GRUB Legacy, to define a value for a command you list the value as a command-line parameter:
                                        
            


            