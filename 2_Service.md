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

    