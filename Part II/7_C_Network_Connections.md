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
                
            
