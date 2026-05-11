# Troubleshooting the Network
    - First identify symptoms, review recent network configuration changes, and formulate potential problem cause theories. Next, using the Open Systems Interconnection (OSI) model as a guide, look at hardware items, proceed to the Data Link Layer, continue to the Network layer, and so on.

    # Exploring Network Issues
        - In order to properly create a troubleshooting plan, you need to understand various network configuration and performance components.
        
        # Speeding Thing Up
            - Familiarity with a few network terms and technologies will help you to troubleshoot your network problems and improve its performance.
                * Bandwidth
                    - Bandwidth is a measurement of the maximum data amount that can be transferred between two network points over a period of time.
                * Throughput
                    - Throughput is a measurement of the actual data amount that is transferred between two network points over a period of time.
                * Saturation
                    - Network saturation, also called bandwidth saturation, occurs when network traffic exceeds capacity.
                * Latency 
                    - Latency is the time between a source sending a packet anf the packet's destination receiving it.
                * Routing
                    - Routers contain buffers that allow them to hold onto network packets when their outbound queues become too long.
                    - However, if the router cannot forward its IP packets in a reasonable time frame, it will drop packets located in its buffer.
        
        # Dealing with Timeouts and Losses
            - A packet drop, also  called packet loss, occurs when a network packet fails to reach its destination.
            - User Datagram Protocol (UDP) does not guarantee packet delivery. Therefore, in servivces like VoIP that employ UDP, minor packet loss does not cause any problems.
            - TCP guarantees packet delivery and will retransmit any lost packets. Thus, if network packet loss occurs for services employing TCP, it will experience delays. 
            - If the packet drops are due to network traffic congestion, in some cases, the TCP packet retransmission only makes matter worse.
            - In network communication, timeouts are typically preset time periods for handling unplanned events.
                - You may experience network communication timeouts for a number of reasons:
        
        # Resolving the Names
            - The process of translating between a system's fully qualified domain name(FQDN) and its IP address is called name resolution.
            - The Domain Name System is a network protocol that uses a distributed database to provide the needed name resolutions.
            - There are few additional items concerning name resolution problems and performance that you need to know.
                * Name Server Location; with client-side DNS, when it comes to name server selection, location matters.
                * Consider Cache; A caching-only name server holds recent name resolution query results in its memory.
                * Secondary Server; If you are managing a DNS server for your company, besides a primary server, consider configuration a secondary server.
        
        # Configuring It Right
            * Interface Configurations; Being able to view a NIC's configuration and status is important in the troubleshooting process.
                - You may need o view its IP address, its MAC address, subnet configuration, error rates, and so on.
                - Be aware that if you use Network Manager on a system with firewalld as its firewall service, when a new network device is added, it will automatically be added to the firewalld default zone.
            * Ports and Sockets
                - Ports and sockets are important structures in Linux networking.
                - Understanding the difference between the two will help in the troubleshooting process.
            * Localhost vs. a Unix Socket
                - The localhost designation and a Unix socket are often used for services, such as SQL.
                - Localhost is the host name for the local loopback interface.
                - Unix sockets, also called Unix domain sockets, are endpoints similar to network sockets. Instead of between systems over a network, these endpoint sockets are between processes on your local system.
            * Adapters
                - Network adapters are system hardware that allows network communications. These communications can be wired or wireless.
                - Adapters also come in USB form factors but are not typically used in enterprise server environments.
            * RDMA( Remote Direct Memory Access)
                - A technology to consider, if your system's network needs low latency, is RDMA.
        
        # Viewing Network Performance
            - Starting the troubleshooting process requires knowledges of the various tools to use.
            - Since high latency(slowness) and network saturation tend to occur together, Table 20.1 shows tools you should use to tackle or monitor for these problems.
            - High latency is sometimes caused by overloaded routers. Faulty hardware or improper configurations, such as the router's MTU being set too low. also contribute to the problem.
            - If you have a rather tricky network problem, it may be worth your while to directly look at the packets traveling over it.
                - The tools to do so go by variety of names: network sniffers and packet analyzers. Three popular ones are Wireshark(GUI program), tshark(terminal-based wireshark), and tcpdump.
    
    # Reviewing the Network's Configuration
        - In the network troubleshooting process, you might want to check your various network configurations.
        - Within a local network segment, routers do not use an IP address to locate systems. Instead they use the system's network adapter's media access control (MAC) address.
        - Incorrect DNS information for your own servers is troublesome. Also if you are considering changing your client-side DNS configuration, there are some utilities that can help you investigate slow query responses.
        - The Network Mapper(nmap) is often used for penetration testing.
        - There are a number of different scans you can run with nmap. You can use nmap to scan entire network segments and ask for the mapper to fingerprint each system in order to identify the operating system running there via the -0 option.

# Troubleshooting Storage Issues
    # Running Out of Filesystem Space
        - Nothing can ruin system uptime statistics like application crashes due to drained disk space. 
        - Two utilites that assist in troubleshooting and monitoring filesystem space are the du and df commands.
            - The df utility allow you to view overall space usage.
            - After you find potential problem subdirectories, start digging down into them via du to find potential space hogs.
            - If you find that the filesystem actually needs the disk space it is using, the only choice is to add more space.
            - If you don't have an extra physical volume in your volume group to add to the filesystem volume needing disk space, do the following;
                - Add a spare drive to the system, if needed.
                - Create a physical volume with the pvcreate command.
                - Add the new physical volume to the group with vgextend.
                - Increase the logical volume size by using the lvextend command.
    
    # Waiting on Disk I/O
        - If a disk is experiencing I/O beyond what it can reasonably handle, it can slow down the entire system.
        - You can troubleshoot this issue by using a utility that displays I/O wait times, such as the iostat command.
            iostat [OPTION] [INTERVAL] [COUNT]
        - There are a few useful iostat options to use for troubleshooting:
            -y, -N, -z, -p device
        - For problems with high I/O, besides employing different disk technologies, you will want to review the Linux kernel's defined I/O scheduling. I/O scheduling is a series of kernel actions that handle I/O requests and their associated activities.
        - If you determine that due to hardware limitations, a new and different hard drive is needed to handle the required I/O levels, the ioping utility can help you in the testing process.
    
    # Measuring Disk Performance
        - One benchmark that's helpful in determinig the overall I/O performance for disk drives is the input/output operations per second (IOPS) value.
        - This value is the number of input or output operations a storage device can perform in a second.
        - A popular tool in the Linux environment for determining IOPS values is the flexible I/O tool, called fio.
        - The tool is available as the fio package in both the Debiean-based and Red Hat-based software repositories, and it must be installed manually.

    # Failiing Disk
        - When a bad sector is marked, typically the controller's firmware will attempt to move the data from the marked sector to a new location and remap the logical sector to the new sector.
        - A random bad sector does not indicate a drive is failing. However, if you are seeing bad sectors more and more on your disk, then it needs to be replaced. 
        - Occasionally a file on the drive loses its matching inode number, called a mismatch, or some other type of disk corruption occurs. 
        - This leaves the data in place, but nothing can access it, and the problem must be repaired manually.
    
# Troubleshooting the CPU
        - You need to correcly size your CPU(s) for your server application needs.
        - For troubleshooting, you need to understand your CPU(s) hardware - the number of cores, whether or not hyperthreading is used, cache sizes, and so on. You can easily view your system's current processors' information.
        - Use the less utility and pass it the /proc/cpuinfo filename.
        - To look at CPU usage, you can employ the uptime command.
        - If you need to view CPU performance over time, the sar utility is useful. The sar utility uses data stored by the sadc program in the /var/log/sa/ directory, which contains up to a month's worth of data.
        - If your server is running multiple virtual machines, the %steal column of the sar utility output is handy.

# Troubleshooting Memory
    - Processes use random access memory to temporarily store data because it is faster to access than data stored on a disk. 
    - One form of this is disk buffering, which improves disk read performance. Data is read from the disk and stored for a period of time in a memory location called a buffer cache.
    - You can see detailed information concerning your system's RAM by viewing the /proc/meminfo file. To view shared memory segments, use the ipcs -m command.

        # Swapping 
            - Memory is divided up into chunks called pages. When the system needs more memory, using a memory management schemem it takes an idles process's memory pages and copies them to disk.
            - This disk location is a special partition called swap space or swap or virtual memory.
            - If the idle process is no more, its memory pages are copied back into memory.
            - If your system does not hace properly sized memory, you should see high RAM usage via the free command.
            - A useful utility for viewing memory and determiining if swap is a file or a partition is the swapon -s command.
            - If you obtain the same information from the /proc/swaps file.
            - For a new partition swap space, once you've created a new disk partition, use the mkswap command to "format" the partition into a swap partition.
            - as swap partition is prepared activate it using swapon command. The free command provide a simple view of your current free and used memory.
            - You must first use the swapoff command on the swap partition to disengage it from swap space. After that the swapon -p priority is used to change the preference priority. You can set priority to any number between 0 and 32767.
            - If all is well with the new swap partition, add it to the /etc/fstab file so it is persistent through system reboots.
        
        # Running Out of Memory
            - By default, the Linux kernel allows itself to overcommit memory to various processes.This is done for efficiency and performance.
            - However, due to this allowance, the system can become very low on free memory. In a critical low-memory situation, Linux first reclaims old memory pages.
            - When triggered, the OOM killer scans through the various proceses using memory and creates a score. 
            - You can force the kernel to prevent memory overcommit via the sysctl command, changing the vm.overcommit_memory kernel parameter from its default of 0 to 1. However, this may not be the best solution.
    
# Surviving a Lost Root Password
    - The quick fix is to reset it via the passwd command using your own account's super user privileges. However, if you were using the root account to gain super user privileges ( which is a bad practice) or your privileges do not allow you to change the root password, you are in trouble. But all hope is not lost.
    - On older Linux distros and a few modern ones (Ubuntu), booting the system into single-user mode will allow you to access the root account and change its password via the passwd command. To do so follow the steps in the book.