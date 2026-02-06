# What is a Linux Server
    <!--Linux Server and Desktop uses the linux Kernel, to run the same shells and also has the ability to run the same program. -->

# Linux Desktop:
    Primarily focus on personal programs that you run from a graphical desktop interface.

# Linux Server
    Primarily operates without human interaction. There's no sitting at a desktop launching applications, it runs program that provide shared resources( called services) to multiple users(clients), normally in a network environment.
    - Rely on CLI, to interact with server administrator, and often the administrator connect remotely(SSH) from clients to perform any interactive work with the services.


# LAUNCHING SERVICE
    There are 2 primary ways linux servers run service programs;
        - As a background process, running at all times listing for requests, this is called DAEMON.
        - As a process spawned by a parent program that listens for the requests.

# SUPER-SERVERS
    These are programs that listen for network connections for several different applications, and when a request is received for a service, it spawn the appropriate service program. The first super-server is called Internet Daemon(inetd) application. IT is also a DAEMON.

# LISTENING TO CLIENT
    Each service whether running from a daemon or a super-server, uses a separate network protocol to communicate with its clients. 
        Network protocol for a service defines exactly how network clients communicate with the service using preassigned port.
                <!--Port are define using the TCP(Transmission Control Protocol) and UDP(User Datagram Protocol) Standard.(It help separate network traffic going through the same IP address).-->
    
### CLIENT USES SAME IP ADDRESS TO CONTACT SERVER BUT DIFFERENT PORT FOR SERVICE.


# SERVING THE BASICS
        # WEB SERVER
            <!--Linux-based web servers host the majority of websites, including many of the most popular websites-->

                #Apache Server
                    Each feature of apache is built as a plug-in module, server administrator can pick and choose just which module, a particular server needs for a particular application.
                
                #Nginx Server
                    It was designed to have apache server feature built-in to increase performance.
                
                                <!-- NOTE: One COnfiguration is using nginx web server as a load-balancer front-end to multiple apache web servers on the back-end. -->

                #lighthttpd package
                    This is a lightweight web server use to process incoming client requests for a network application. Able to combine web and database service in a single package.

            
            
            
        # DATABASE SERVER
            <!-- Relational database allowed applications to quickly store and retrieve data 
                 SQL provides a common method for clients to send request to the database server and retrieve the data.-->
        
                #POSTGRESQL SERVER
                    Objective was to implement a complete object-relational database management system to rival the popular commercial database server, but it defect is his speed.

                #MYSQL SERVER
                    Offers basic feature that performs quickly. MySQL, apache server, php language known as LAMP platform. 
                        Overtime implement feature that rival those found in Postgresql and commercial databases.
                
                # MangoDB Server( Store data as JSON)
                    NoSQL database system stores data differently then the traditional relational database system using SQL.
                        It does create table but stores data as individual documents. Each data element being independent from the other data elements in the database. MangoDB has no security.
                
        # MAIL SERVER
            <!-- Instead of having  one monolith program that handles all of the pieces required for sending and receiving mail, linux uses multiple small programs that work together in the processing of email messages. The MUA interact with client which exclude it from the server while MTA and MDA are in the linux server-->

                    # The mail transfer agent ( MTA )
                            The MTA is responsible for handling both incoming and outgoing email messages on the server. 
                            
                            **MTA software packages**
                                #Sendmail: 
                                - The sendmail MTA package is versatile. 
                                - Most of the features in sendmail are synonymous with email systems(virtual domains, message forwarding, user aliases, mail lists, host masquerading).
                                - Its configuration is very complex.

                                #Postfix:
                                - The Postfix MTA was written as a modular application, using several different programs to implement the MTA functionality.
                                - It uses two small configuration( plaintext parameters and value names to define the functionality.).

                                #Exim:
                                - Exim package just as the sendmail uses a monolith program to handle all the email functions.
                                - Attempt to avoid queuing messages as much as possible, instead relying on immediate delivery in most environments.

                    # The Mail Delivery agent( MDA )
                            Linux implementations rely on separate stand-alone mail delivery agent ( MDA ) programs to deliver messages to local users.

                            **MDA Programs**
                                #Binmail:
                                -Location: /bin/mail.
                                - It is simple and can read email messages stored in the standard /var/spool/mail directory or can point it to an alternative mailbox.

                                #Procmail:
                                - Versatile in creating user-configured recipes that allow a user to direct how the server processes received mail.
                    
                    # The Mail User Agent( MUA )
                            - Most software packages are available in linux for reading and sending mail. 
                            - Most remote client packages use Internet Message Access Protocol Version 4(IMAP4) to communicate with email server and work with email messages.
                            - To support IMAP4 client linux uses IMAP4 server an example is Dovecot.

# Serving Local Networks

    # File Servers
        
        # Peer-to-peer
                - Here, one workstation connects locally to another workstation to allow the sharing of files stored on its hard drive. Becomes complex when more than 2 computers are involved.

        # CLient-server
                - Client-server method of file sharing utilizes a centralized file server for sharing files that multiple clients can access and modify.
                - The administrator controls files accessibility, preventing unauthorized access.

    NOTE: IN LINUX THERE ARE TWO COMMON SOFTWARE PACKAGES USE FOR SHARING FILE: NFS and SAMBA

            # Network File System(NFS)
                - NFS is the process of sharing file in a network environment.Here, the linux 
                system shares a portion of its virtual directory on the network, giving access to clients, or other servers.
                - The software package used here is nfs-utils( it handles driver and support client and servers software to both share local folder on network and connect with remote folders).

            # Samba
                - While Windows workstations and servers can use NFS, the default file sharing method used in Windows is the System Message Block(SMB) protocol.
                - SMB protocol authorise the possibility to create open source software that can interact with Windows servers and clients.
                - SAMBA was created to allow linux system to connect to either the Windows server(permitting workstation to connect to its shared folders) or clients(connecting to Windows server shared folders). 
                - It takes some configuration to get it set up.

    # Print Servers
        - Common Unix Printing System(CUPS) is the standard linux print sharing software which allow a linux system to connect to any printer resource(locally/network).
        - The key to CUPS is the Printer drivers, many printers manufacturer create CUPS driver so that the linux system can connect to the printers.
        - IPP( Internet Printing Protocol) is the protocol utilized for network printer.

    # Network Resource Servers <!-- Some of the basic network-oriented service you may see on a linux server-->
       # IP addresses
            - Every device on a local network must have a unique IP address to interact with other devices on the network.
            - DHCP( Dynamic Host Configuration Protocol ) keeps track of the IP Address assigned to a workstation, ensuring that no two workstation receive the same IP address.
            - Once you have a DHCPd server connected to your network, you will need to configure the Linux client to use it to obtain his IP address.

		#logging 
			- Linux maintains log files that record various key details about the system as it runs.
					*rsyslogd
							It is utilized by SysVinit and Upstart systems to accept logging data from remote servers.
					*journald
							The Systemd system utilized journald service for both local and remote logging for system information.

	# Name Servers
			- DNS(Domain Name Server) maps IP address to a host naming scheme on networks.
			- Linux Server uses BIND software package to provide DNS naming service. 

	# Network Manaagement
		- The SNMP( Simple Network Management Protocol) provides a way for an administeator to query remote network devices and servers to obtain information, about their configuration, status and even performance.
		- The most popular SNMP software package in Linux is the open source net-snmp package. This package has SNMPv3 compatibility, allowing you to securely monitor all aspects of a Linux server remotely.
  	
	# Time 
		- For most network applications to work correctly, both servers and clients need to have their internal clocks coordinated with the same time.NTP( Network Time Protocol) accomplishes this.  

# IMPLEMENTING SECURITY
 	# Authentication Server
		- The core security for Linux is the standard userid and password assigned to each individual user on the system and stored in either the /etc/passwd( on non-legacy systems) or the /etc/shadow file.
				<!-- Methods on sharing user account database -->

			# NIS( Network Information System)
				- This is a directory service that allows both clients and server to share a common naming directory.

			# Kerberos
				- It uses symmetric-key cryptography to securely authenticate users with a centralized server database.
			
			# LDAP(Lightweight Directory Access Protocol)
				- the LDAP was created to provide simple network authentication services to multiple applications and devices on a local network.
				- It was design to design a hierarchical database to store objects in your network.
    
			# Certificate Authority
				- A cerificate is an encrypted key that implements a two-factor authentication method. The user must possess;
						* Certicate file	
						* PIN

			# Access Server( SSH)
				- The Secure Shell provides a layer of encryption around data sent accross the network. 
				- The most popular software package that implement SSH in the linux environment is OpenSSH package.
