# Communicating with Linux Devices
    - The kernel uses installed modules to know how to communicate with each type of hardware device on the system. If the module for a particular hardware device isn't loaded, then the kernel won't be able to communicate with the device.
    
    # Device Interfaces
        - Each device you connect to your Linux system uses some type of standard protocol to communicate with the system hardware.
            - There are currently three popular standards used to connect devices.
        
        # PCI Boards
            - The Peripheral Component Interconnect(PCI) standard was developed as a method for connecting hardware boards to PC motherboards. 
            - The PCI Express standard is currently used on most server and desktop workstations to provide a common interface for external hardware cards.
            - Lots of different client device use PCI boards to connect to a server or desktop workstation:
                * Internal hard drives, External hard drives, Network Interface cards, Wireless cards, Bluetooth devices, Video accelerators, Audio cards
        
        # The USB Interfaces
            - The USB interface has become increasingly popular due to its ease of use and its growing support for high-speed data communication.
            - Since the USB interface uses serial communications, it requires fewer connectors with the motherboard allowing for smaller interface plugs.
        
        # The GPIO interface
            - The General Purpose Input/Output (GPIO) interface has become popular with small utility Linux systems designed for controlling external devices for automation projects.
            - This includes popular hobbyist Linux systems such as the Raspberry Pi and BeagleBone kits.
            - The GPIO interface provides multiple digital input and output lines that you can control individually, down to the single-bit level.
    
    # The /dev Directory
        - After the Linux kernel can communicate with a device on an interface, it must be able to transfer data to and from the device.
        - Device files are files that the Linux kernel creates in the special /dev directory to interface with hardware devices.
        - To retrieve data from a specific device, a program just needs to read the Linux device file associated with that device.
        - There are two types of device files in Linux, based on how Linux transfers data to the device:
            * Character device files: Transfer data one character at a time. This method is often used for serial devices such as terminals and USB devices.
            * Block device files: Transfer large blocks of data. This method is often used for high-speed data transfer devices such as hard drives and network cards.
        - There are also few character device files that provide useful features for the shell. Ones of note are
            * /dev/null: When data is redirected to this device, the data is discarded.
            * /dev/randon and /dev/urandom: These devices files provide access to the kernel's random number generator. The /dev/random device blocks requests until enough random data has been generated to calculate a true random number.
                - The /dev/urandom device doesn't block, but just returns a random number using the random data currently available.
            * /dev/zero: When data is read from this device, it returns a NULL character. This is an excellent resource for creating null files or erasing previously stored data on a disk partition.
    
    # The /proc Directory
        - The /proc directory is one of the most important tools you can use when troubleshooting hardware issues on a Linux system.
        - It is not a physical directory on the filesystem but instead a virtual directory that the kernel dynamically populates to provide access to information about the system hardware settings and status.
        - There are different /proc files available for different system features, including the IRQs, I/O ports, and DMA channels in use on the system by hardware devices.
            # Interrupt Requests
                - Interrupt requests(IRQs) allow hardware devices to indicate when they have data to send to the CPU. The PnP system must assign each hardware device installed on the system a unique IRQ address.
                - You can view the current IRQs in use on your Linux system by looking at the /proc/interrupts file using the Linux cat command.
            #I/O Ports
                - The system I/O ports are locations in memory where the CPU can send data to and receive data from the hardware device.
                - As with IRQs, the system must assign each device a unique I/O port.
                - You can monitor the I/O ports assigned to the hardware devices on your system by looking at the /proc/ioports file.
            # Direct Memory Access
                - Using I/O ports to send data to the CPU can be somewhat slow. To speed things up many devices use DMA channels.
                - They send data from a hardware device directly to memory on the system, without having to wait for the CPU. The CPU can then read those memory locations to access the data when it's ready.
                - To view the DMA channels currently in use on the system, just display the /proc/dma file:
    
    # The /sys Directory
        - The /sys directory provides additional information about the hardware devices that any user on the system can access.
        - You can take a look at the subdirectories and files available within the /sys directory on your system using the ls command-line command.
    
# Working with Devices
    # Finding Devices
        /*One of the first tasks for a new Linux administrator is to find the different devices installed on the Linux system.*/

        # The lsdev command
            - The lsdev command-line command displays information about the hardware devices installed on the Linux system.
            - It retrieves information from the /proc/interrupts, /proc/ioports, and /proc/dma virtual files and combines them in one output.
        
        # The lsblk command
            - The lsblk command-line command displays information about the block devices installed on the Linux system. 
            - By default, the lsblk command displays all of the block devices. The lsblk command also indicates blocks that are related, as with the device-mapped LVM volumes and the associated physical hard drive.
        
        # The dmesg command
            - The kernel ring buffer records kernel-level events as they occur. Since it's ring buffer, the event messages overwrite after the buffer area fills up.
    
    # Working with PCI Devices
        - The lspci command allows you to view the currently installed and recognized PCI and PCIe devices on the Linux system.
        - There are lots of command-line options you can include with the lspci command to display information about the PCI and PCI cards installed on the system.
        - The output from the lspci command without any options shows all devices connected to the system.
    
    # Working with USB Devices
        - You can view the basic information about USB devices connected to your Linux system by using the lsusb command.
        - Most systems incorporate a standard USB hub for connecting multiple USB devices to the USB controller.
    
    # Supporting Monitors
        - There are two basic elements that control the video environment on your Linux system: the video card and the monitor.
        - To display any type of text or graphics, your Linux system must know how to interact with both of them.
        - The X Window System was developed at the Massachusetts Institute of Technology(MIT) to provide a standard protocol for interacting with displays.
        - The original X11 software for Linux was XFree86 package. This was notorious for being difficult to configure and get working with differnt types of video hardware. 
        - Because of that, newer X11 packages have surfaced and have become more common:
            * X.org: A user-friendly X11 software package for Linux, develped as a direct replacement for XFree86, but using simple text-based configuration files. Stored /etc/X11 directory.
            *Wayland: A simpler, more secure graphical software package, developed by Red Hat, and released as open source software.
    
    # Using Printers
        - With different types of printers available, trying to install the correct printer drivers as well as using the correct printer protocol to communicate with them can be a nightmare.
        - CUPS( Common Unix Printing System) solves many of those problems for us. CUPS provides a common interface for working with any type of printer on your Linux system.
        - It accepts print jobs using the PostScipt document format and sends them to printers using a print queue system.
        - The CUPS software uses the Ghostscript program to convert the PostScript document into a format understood by the different printers.
        - To define a new printer on your Linux system you can use the CUPS web interface.
        - Aside from the CUPS web interface, there are a few command-line tools you can use for interacting with the print queues:
            * lpc: Start, stop or pause the print queue.
            * lpq: Display the print queue status, along with any print jobs waiting in the queue.
            * lpr: Submit a new print job to a print queue.
            * lprm: Removea specific print a job from the print queue.
            
# Using Hot-Pluggable Devices
    - Computer hardware is generally categorized into two types:
    - Cold-pluggable devices are hardware that can be connected to the system only when the system is completely powered down. These usually include things commonly found inside the computer case, such as memory, PCI cards, and hard drives. You can't remove any of these things while the system is running.
    - Conversely, you can usually add and remove hot-pluggable devices at any time. These are often external components, such as network connections, monitors, and USB devices. The trick with hot-pluggable devices is that somehow the Linux kernel needs to know when the device is connected and automatically load the correct device driver module to support the device.

    # Detecting Dynamic Devices
        - The udev device manager is a program that is automatically started at boot time by the init process( usually at run level 5 via the /etc/rc5.d/udev script) or the Systemd systems and runs in the background at all times.
        - It listens to kernel notifications about hardware devices. As new hardware devices removed, the kernel sends out notification event messages.
        - The udev program listens to these notification messages and compares the messages against rules defined in a set of configuration files, normally stored under the /etc/udev/rules.d directory.
    
    # Working with Dynamic Devices
        - While the udev program runs in the background on your Linux system, you can still interact with it using the udevadm command-line tool. The udevadm command allows you to send commands to the udev program.
        - The format of the udevadm command is as follows:
            udev command [OPTIONS]
        - The control command allows you to change the currently running udev program.
        
