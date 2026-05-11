/* A firewall in a building is a fireproof wall that helps to prevent fire from spreading throughout the structure. In Computer security, firewalls prevent the spread of unwanted, unauthorized, or malicious network traffic.*/

# Provifing Access Control
    - An access control list(ACL) implemented with a firewall identifies which network packets are allowed in or out. Refered as packet filtering.
    - A firewall ACL identifies a network packet by reviewing its control information along with other network data.(Source address, Destination address, Network protocol, Inbound port, Outbound port, Network state)
    - Once a network packet is identified, the firewall's ACL rules also determine what happens to that packet.(Accept, Reject, Drop, Log)
    - On Linux, the /etc/services file documents the different standard application services names and their corresponding port numbers and protocols as well as any aliases. This service catalog is used by various utilities such as the netstat network tool, and firewall applications, such as UFW, to determine the appropriate port and protocol information for a particular service.
    - Each non-comment record in the /etc/services file uses the following syntax:
        ServiceName PortNumber/ProtocolName [Aliases]
    - By default, port number 1 through 1023 are privileged port.
    - Firewalls can operate in either a stateful or statelss manner. There are pros and cons to both technologies.
        - Stateless: This technology is the older of the two. In this mode, the firewall focuses only on individual packets.
        - Stateful: This technology is the younger of the two. While it also employs packet filtering, it does not treat packets as individuals, but instead as a stream.
    
# Looking at Firewall Technologies
    - Embedded in the Linux kernel is netfilter. This software provides code hooks into the kernel, which allo other packages to implement firewall technologies. 
    - From a functionality standpoint, think of netfilter as a network sniffer that is planted in the Linux kernel and offers up packet filtering services.
    - Another firewall technology that uses netfilter is firewalld. The newer firewalld service allows modified filter rules to be updated dynamically with no need t restart the service.
        - For Red Hat-based distro, you configure your network environment during the installation it will install the firewalld service by default.
        - Debian-based distro use yet another firewall service that utilizes netfilter: the Uncomplicated Firewall(ufw). This firewall configuration tool is an interface to the netfilter firewall that provides easier rule management.

    # Familiarixing Yourself with firewalld
        - The firewalld service provides packet filtering and user interfaces for the GUI environment and the command line. 
        - It offers support for IPv4 as well as IPv6 and much more.
        - This firewall service is called the dynamic firewall daemon because you can change an ACL rule without needing to restart the service. The rules are loaded instantaneously via its D-Bus interface.
        - A central part of firewalld is zones. Network traffic is grouped into a predefined rule set, or zone. Each zone has a configuration file that defines this rule set, also called a trust level.
        - By default, firewalld zone configuration files are stored in the /usr/lib/firewalld/zones/ directory. Customized or user-crated zone configuration files are stored in the /etc/firewalld/zones/ directory.
        - The firewall-cmd utility allows you to view and interact with various firewalld configuration settings. NetworkManager is also integrated with firewalld.
        - A service is a predefined configuration set for a particular offered system service, such as DNS. The configuration information may contain item such as a list of ports, protocols, and so on.
    
    # Investigating iptables
        - The iptables firewall service uses a series process called chains to handle network packets that enter the system. 
        - The chains determine the path each packet takesas it enters the Linux system to reach the appropriate application. As an application sends packets back out to the network to remote clients, these chains are also involved.
        - There are five separate chains to process packets:
            * PREROUTING : handles packets before the routing decision process.
            * INPUT: handles packets destined for the local system.
            * FORWARD: handles packets being forwarded to a remote system.
            * POSTROUTING: handles packets being sent to remote systems, after the forward filter.
            * OUTPUT: handles packets output from the local system.
        - Each chain contains tables that define rules for handling the packets. There are five table types:
            * filter: applies rules to allow or block packets from exiting the chain.
            * mangle: applies rules to change features of the packets before they exit the chain.
            * nat: applies rules to change the addresses of the packets before they exit the chain
            * raw: applies a NOTRACK setting on packets that are not to be tracked.
            * security: applies mandatory access control rules.
        - Implementing network address translation (NAT) requires using the nat table to alter the packets' address in the OUTPUT chain.
        - Each chain has a policy value; ACCEPT and DROP.
        - As long as the iptables service is enabled to start at system boot, Red Hat and it's distro will automatically load iptables rules files:
            * IPv4 rules: /etc/config/iptables
            * IPv6 rules: /etc/config/ip6tables
        - Debian and Debian-based distributions need an additional software package, iptables-persistent, installed and enabled. The files this package uses to load persistent rules are as follows:
            * IPv4 rules: /etc/iptables/rules.v4
            * IPv6 rules: /etc/iptables/rules.v6
        - If you need to save the current iptables rules, employ the iptables-save command. This utility needs its output redirected to a fil because by default, it sends the rules to STDOUT.

    # Noticing nftables
        - You may have noticed that the format to create rules in iptables can often get somewhat complicated, especially compared to tools like firewalld. A good compromise is the nftables service.
        - The nftables service provides low-level access to the netfilter chains similar to iptables, making it extremely efficient and fast.
        - the nftables service uses the same concept of tables, chains, policies, and rules as iptables.
        - The type value can befilter, router, or nat, the hook value can be prerouting, input, forward, outputor postrouting(again the same as in iptables).
        - The priority value determines the order in which the chain is processed; lower-priority values are processed first. The policy value can be either accept or drop.
    
    # Understanding ufw
        - The uncomplicated Firewall(ufw) is the default firewall service on Ubuntu distributions. 
        - It is configured with the ufw command-line utility or gufw for the GUI.
        - There are several ufw commands that control the firewall's stateas well as view its status. Each one requires super user privileges.
        - Viewing the verbose status of the ufw firewall provides information that helps to explain its configuration:
            * Status, Logging, Defaul, New profiles
        - The various default ufw polices are stored in the /etc/default/ufw configuration file. When first installed, these settings allow all outgoing connections and block all incoming connections.
        - You can make modifications to the firewall as needed using the ufw command and its various arguments.
        - View any user-added rules using the ufw show added commmand. The ufw rules are stored in the /etc/ufw/ directory, and user-added rules are placed into the user.rules file within that directory.
        - The ufw service uses profiles for common applications and daemons. These profils are stored in the /etc/ufw/applications.d/ directory. Use the ufw app list command to see the currently available UFW application profiles.
    
    # Forwarading IP Packets
        - There is a packet-forwarding feature in Linux. This feature is used for various purposes, such as allowing Linux to forward packets to a remote host or for IP masquerading.
        - You must enable packet forwarding in the kernel before employing it. To enable that feature, just set the ip_forward entry for IPv4 or the forwarding entry for IPv6.
        - You can check the current kernel values by using the cat command in the /proc filesystem entries.
        - Once those kernel values are set, your Linux system is able to forward traffic from one network interface to another network interface. 
        - IP forwarding is most commonly used in IP masquerading, which is when you want to hide your internal IP addresses when communicating with the outside world.
        - In this scenario, the firewall receives packets from the internal network on the one network interface, and then, on a separate network interface connected to an external network, it sends all outbound packets using the same IP address, but using differnt port numbers.
        - To enable NAT, you need to have IP forwarding enabled; then you need to tell the firewall service to masquerade your outbound packets as a different IP address.

    # Dynamically Setting Rules
        - In protecting your system, it helps to have software that monitors the network and applications running on the system, looking for suspicious behavior.
        -THese application are called intrusion detection systems(IDSs). Some IDS applications allow you to dynamically change rules so that these attacks are blocked. 
        # DenyHosts 
            - The DenyHosts application is a Pythin script, which helps protect against brute=force attacks coming through OpenSSH.
            - The script can be run as a service or as a cron job.

        # Fall2ban
            - The Fail2ban service also monitors system logs, looking for repeated failures from the same host.
            - If it detects a problem, Fail2ban can block the IP address of the offending host from accessing your system.
            - The fail2ban-client program monitors both system and application logs looking for problems. It monitors common system log files such as /var/log/pwdfail and /var/log/auth.log log files, looking for multiple failed login attempts.
            - A great feature of Fail2ban is that it can also monitor individual application log files, such as the /var/log/apache/eror.log log file for the Apache web server.
            - The /etc/fail2ban/jail.conf file contains the Fail2ban configuration. It defines the applications to monitor, where their log files are located, and what actions to take if it detects a problem.
        
        # IPset
            - An IPset is a namd set of IP addresses, network interfaces, ports, MAC addresses, or  subnets.
            - By creating these sets, you can easily manage the groupings through your firewall and any other application that supports IPsets.
            - The ipset utility is used to manage IPsets and requires super user privileges. When you create an IPset, you need to first determine what name you will give it.
            - After that, decide how you want the IPset to be stored. Your storage choices are bitmap, hash,or list.
                ipset create IPset-Name storage-method:set-type
                ipset -N IPset-Name storage-method:set-type
    