# Configuring Network Features
    - There are 5 main pieces of information you need to configure in your Linux system to interact on a network:
        - The host address
        - The network subnet address
        - The default router(sometimes called gateway)
        - The system hostname
        - A DNS server address for resolving hostnames
    - The ways to configure this information in Linux systems:
        # Manually editing network configuration files. - No need in this generation.
        # Using a graphical tool included with your Linux distribution: Graphical Tools
            - The Network Manager tool provide a graphical interface for defining network connections.
            - If your system detects a wired network connection, the icon appears as a mini-network with blocks connected together. If your system detects a wireless network connection, the icon appears as an empty radio signal.
            - You can select the network connection to configure and then click the Edit button to change the currentt configuration. Automatically update by Network Manager.
        # Using command-line tools - Command-Line Tools
            # Network Manager Command-Line Tools
                - nmtui, a simple text-based menu tool
                    - Displays a stripped-down version of the graphical tool where you can select a network interface and assign network properties to it.
                - nmcli, a text-only command-line tool
                    - It provides a command-line interface where you can view and change the network settings.
            
            # The Netplan Tool
                - It doesn't configure network settings itself, but instead provides an easy way to specify network settings in a YAML file. It interpret those settings and create standard Network Manager configuration lines. /etc/netplan folder with a .yaml extension.
                - Netplan program then allows you to use command options to manage the configuration file.
                    - netplan apply: Applies all configuration file to the appropriate network tools and restarts them if necessary.
                    - netplan generate: Renders the configuration file for the specified network tool.
                    - netplan try: Applies the configuration and waits for a reply by the user. Netplan will roll it back if not work.
            
            # The iproute2 Utilities
                - The iproute2 package is an open source project that contains a set of command-line utilities for managing network connections.
                - Each command option uses parameters to define what to do.
                # The local loopback interface is a virtual network interface that permit any local program to use it to communicate with other programs just as if they were across a network.
                # The enp0s3 network interface is the wired network connection for the Linux system. The ip command shows the IP address assigned to the interface( both IP and an IPv6 link local address assigned),   the netmask value, and some basic statistics about the packets on the interface. If the output doesn't show a network address assigned to the interface, you can use the ip command to specify the host address and netmask value for the interface:
                    # ip address and 10.0.2.15/24 dev enp0s3
                Then use the ip command with the route option to set the default router for the network interface:
                    # ip route add default via 192.168.1.254 dev enp0s3
                Finally, make the network interface active by using the link option:
                    # ip link set enp0s3 up
            
            # The net-tools Legacy Tool
				- The net-tools package was the original method in Linux for managing individual aspects of the network configuration. There are 5 main command you need to use:
					- ethtool; displays Ethernet settings for a network interface.
						- Allows to peak inside the network interface card Ethernet settings and change any properties that you may need to in order to communicate with a network device, such as a switch.
					- ifconfig; displays or sets the IP address and netmask values for a network interface.
						- You can also use it to view current statistics for a network interface, you can also see the link status of a network interfae, whether it is receiving or transmitting packets.
						
					- arp; allows you to display, add, or delete entries in the system Address Resolution Protocol (ARP) table.
						- 
					- iwconfig; sets the SSID and encryption key for a wireless interface.
						- If you are working with wireless network card, you must assign the wireless SSID and encryption key values using the iwconfig command:
							# iwconfilp6s0 essid "MyNetwork" key s:mypassword
						- Use the iwlist to display all of the wireless signals your wireless card detects.
					- route; sets the default router address.
						- You must also set the default router using the separate route command:
							# route add default gw 192.168.1.254
								- route command by itself to view the current default router configured for the system.
								- You can create the routing table in the system by using the add or del command-line option for the command; route [add] [del] target gw gateway
								- Where target is the target host or network and gateway is the router address.
				
			# Additional Network Features
				- You need to ensure that a proper DHCP client program is running on your Linux system, if your network uses DHCP.
				- The DHCP client program communicates with the network DHCP server in the background and assigns the necessary IP address settings as directed by the DHCP server.
					- dhcpcd; program the most popular, When you use the Linux system's software package manager utility to install the DHCP client program, it sets the program to automatically launch at boot time and handle the IP address configuration needed to interact on the network.
						- Bonding(network interface bonding) allows you to aggregate multiple interfaces into one virtual network device.
							You can tell the Linux system how to treat the virtual network device using three different bonding types:
								- Load balancing: Network traffic is shared between two or more network interfaces.
								- Aggregation: Two or more network interfaces are combined to create one larger network pipe.
								- Active/passive: One network interface is live while the other is used as a backup for fault tolerance.
							To initialize network interface bonding, you must first load teh bonding module in the Linux kernel; Then define the network interface using ip utility: add the appropriate network interfaces to the bond using the ip utility: The Linux system will then treat the bond device as a single network interface depending on the mode you defined.
					- dhclient
				pump
		# Command-Line Networking Tools
			# The netcat Tool
				- It act as either a network server or network client, sending and receiving data packets using either TCP or UDP.
				- Available on either "netcat" or "nc" depending on Linux distribution.
						syntax: nc host port
				- By default, netcat will attempt to establish a TCP connection with the remote server.
				- Can be use to transfer a file from one system to another. just redirect the output of the listening host to a file.
				- These files are not secured, the s_client package allows you to test secure SSL connections with a network server.

			# The cURL Tool
				- It allows you to transfer data to or from a remote server using a standard URL address commonly used in browsers. It supports a wide range of connection types, FTP, FTPS, HTTP,HTTPS, IMAP, IMAPS, SMTP, SMTPS, Telnet, and TFTP.
				
								
				


































                
            
