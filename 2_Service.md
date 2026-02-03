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

    # Network Resource Servers
       # IP addresses
            - Every device on a local network must have a unique IP address to interact with other devices on the network.
            - DHCP( Dynamic Host Configuration Protocol ) Controls the 
        
    





    
