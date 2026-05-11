# User Security

    # Authentication Methods
        - The standard user ID/password combination has been used for decades in server environments. Unfortunately there are limitations to the user ID/password authentication method.
        - Because of some of these limitations, Linux administrators have been using other authentication methods.

            # Kerberos
                - With SSO, you need to log into the network only once to access any server on the network.
                - Three pieces are involved with Kerberos authentication process:
                    * Authentication server(AS): Users log into the AS to initiate the authentication process. The AS acts as the traffic cop, directing the log process through the multiple Kerberos servers involved.
                    * Key distribution center (KDC): The AS passes the login request to the KDC, which issues the user a ticket-granting ticket(TGT) and maintains it on tje server.
                    * Ticket-grunting service (TGS): After the KDC issues the user a ticket, the user can log into servers on the network that support the Kerberos system.
                - Kerberos centralizes the authentication process but still requires individual servers to maintain their own database of what objects on the server the user account has access to.
            
            # LDAP
                - LDAP uses a hierarchical tree database structure to store information about both network users and resources.
                - Network administrators can enter permissions for various network resources into the LDAP database structure.
                - One nice feature of LDAP is that you can distribute the LDAP database among servers on the network.

            # RADIUS
                - As its name suggests, the Remote Authentication Dial-In User Service(RADIUS) is somewhat of an old authentication technology. It was originally created to provide centralized authentication services for dial-up bulletin board servers.
                - The RADIUS protocol allows an authentication server to authenticate not only the user account, but also other information about the user, such as network address, phone number, and access privileges.
            
            # TACACS+
                - The Terminal Access Controller Acces-Control System defines a family of protocols that provide remote authentication in a server environment.
        
        # Multifactor Authentication
            - Over the years other login methods have been developed to help provide a more secure login environment.
                * Biometrics: The most basic form of two-factor authentication is biometrics. Biometrics uses a physical feature that you have to authenticate you.
                * Tokens: Digital tokens store a digital ID as an encrypted file. You must present the file to the server to gain authorization to access the server.
                * Public key infrastructure (PKI): PKI adds a level of complexity and security to tokens by incorporating an asynchronous key environment.
                * One-time passwords: With the one-time password setup, you log into a server using your standard use ID and password, but then the server sends an additional password to the email address or text message that's on file for your user account.
        
        # Unique User Accounts
            - The key to any type of security plan is to know what your authorized user are doing.
            - This helps in detecting rogue users purposely doing harm to the system, and it can help in detecting novice users who accidentally do wrong things.
            - The main goal of monitoring users is nonrepudiation( that every action a user takes can be tracked back to that exact user).

        # Enforce Strong Passwords
            - Password-based authentication is only as good as the passwords your system users use.
            - /etc/login.defs configuration file, defines how the system handles user passwords. Using this file, you can define basic security settings for passwords with the following:
                * PASS_MAX_DAYS: The number of days until a password change is required
                * PASS_MIN_DAYS: The number of days after a password is changed until the password may be changed again.
                * PASS_MIN_LENGTH: The minimum number of characters required in a password.
                * PASS_WARN_AGE: The number of days a warning is issued to the user prior to a password's expiration.
            - These settings apply to the length and age of a password, but not to the complexity, for that you may use PAM authentication services.
            - The pwquality.so library defines password rules that apply to the system user accounts.
            - In Red Hat-based distributions, you define the password quality settings in the /etc/pam.d/system-auth configuration file.
            - The complixity setting directives work using a concept called credits.

        # Restricting the Root Account
            - The root user account is important in that it has complete privileges over all aspects of the Linux system.
            - There are several security best practices for helping restrict just how the root user account is used in your Linux system.
                
                # Completely Blocking Root Access
                    - The su and sudo commands allow any user account to perform administrative jobs without actually logging in as the root user account.
                    - To prevent anyone from logging into the Linux system as the root user account, you can use a trick that involces the /etc/passwd file.
                
                # Blocking Root Access from Specific Devices
                    - For Linux systems that use a console physically attached to the system, you may want to block anyone from walking up to the system and logging in as the root user account.
                    - To do this, create a /etc/securetty file on the system, which list all of the devices the root user account is permitted to log in from.
                
                # Blocking Root Access from SSH
                    - You'll need to modify the OpenSSH program, which provides secure connections to your Linux system.
                    - Edit line: #PermitRootLogin yes
                
# System Security

    # Separation of Data
        - In a multiuser environment, it's always good practice to separate the user data storage from the system storage. When you use two separate partitions, if users fill up their storage partition, the system can still operate in its own storage partition.
    
    # Disk Encryption
        - Instead of encrypting individual files, the solution is to use disk encryption. Disk encryption works at the kernel level and encrypts every file that's stored on the disk partition. You don't need to do anything special from your applications.
        - As you read data from files on the encrypted disk, the kernel automatically decrypts it, and as you write data to files on the encrypted disk, the kernel automatically encrypts them.
        - THe Linux Unified Key Setup (LUKS) application acts as the intermediary when working with files on a filesystem. It uses two components to interface between the kernel and applications:
            * dm-crypt: This moduile plugs into the kernel and provides the interface between a virtual mapped dive and the actual physical drive.
            * cryptmount: The cryptmount command creates the virtual mapped drive and interfaces it with the physical drive via the dm-crypt module.

    # Restricting Application
        - One method of protecting applications from each other is incorporating a chroot jail. The chroot utility runs a command in a new root directory structure, within the standard Linux virtual filesystem.
        - All disk access performed by the command is restricted to the new root directory structure.
            - The format of the chroot utility is 
                chroot starting_directory command
    
    # Preventing Unauthorized Rebooting 
        # Preventing Access to the BIOS/UEFI
            - It's always a good idea to enable the password feature in the BIOS or UEFI software.
            - When a password is assigned, you must enter it to gain access to the BIOS or UEFI menu system to make changes.
        
        # Preventing Access to the GRUB Bootloader
            - You should place a password on the GRUB bootloader system to prevent unauthorized users from accessing the GRUB menu.
            - Since the GRUB configuration files are plaintext, for best security you should encrypt the password value before storing it in the configuration file.
        
        # Disabling the Clrl+Alt+Del Combination
            - For systems that use the SystV int method, the combination is defined in the /etc/inittab file:
                ca::ctrlaltdel:/sbin/shutdown -t3 -r now
            (Read the rest)
            - For systems that use the systemd startup method, you'll need to disable the combination using the systemctl command:
                sudo systemctl mask ctrl-alt-del.target
    
    # Restricting Unapproved Jobs
        - The at and cron utilities allow users to schedule jobs when they're not logged into the system.
        - Both the at and cron utilites provide blacklist and whitelist files for either denying or allowing user accounts to schedule jobs. These files are as follows:
            * /etc/at.allow
            * /etc/at.deny
            * /etc/cron.allow
            * /etc/cron.deny
        - As the filenames suggest, the .allow files contain list of user accounts allowed to schedule jobs, while the .deny files contain lists of user accounts prevented from scheduling jobs.
    
    # Banners and Messages
        - Linux provides multiple ways for you to present canned messages to your system users as they log into the system.
            - /etc/issue: The system displays the contents of the issue file before the login prompt at console logins.
            - /etc/issue.net: The system displays the contents of the issue.net file before the login prompt at network logins.
            - /etc/motd: The system displays the contents of the motd(message of the day) file immediately after the user logs into the console or terminal session.
            - /usr/bin/wall: Allows the system administrator to send interactive messages to all users currently logged into the system.
    
    # Restricting USB Devices
        - When a user plugs in a USB storage device, the kernel automatically looks for a module to support the device.
        - If none is installed, it calls the modprobe utility to automatically load the appropriate kernel module to support the device.
        - The modprobe utility uses configuration files to define how to operates and where it looks for module files.
        - The configutation file is stored in the /etc/modprobe.d directory.
        - When you install a USB storage device, the kernel loads two modules: uas & usb_storage. To prevent that from happening, open the blacklist.conf text file and add these lines:
            * blacklist uas
            * blacklist usb_storage
    
    # Looking for Trouble
        - As a Linux administrator, it's your job to keep up-to-date on what attacks can be made against your Linux system.
        - MITRE maintains a database of published CVE events and assigns each entry with unique CVE Identifier.
        - Several tools are available for scanning Linux systems to look for vulnerabilities listed in the CVE. The Security Content Automation Protocol (SCAP), and the OpenSCAP package provides a toolset for scanning Linux systems looking for vulnerabilities defined by SCAP.
        - Two more common tools for the Linux environment are the Advanced Intrusion Detection Environmnet(AIDE) and Rootkit hunter (rkhunter).
    
    # Auditing
        - The standard system logs available on your Linux system provide a wealth of information on what's going on in your Linux system, but the don't quite cover everything
        - Tracking this type of information requires a more robust security auditing system above the standard rsyslog log events. The auditd package provides the extra level of logging for us.
        - The auditd package allows you to define your own set of security rules to monitor and log lots of different types of system events, such as the following events:
            * File and directory access by users
            * System calls made by applications
            * Specific commands run by users
            * Network access by users
            * Network connection attemps made by external hosts
        - You defin events to monitor by creating rules. There are three types of rules you can create:
            * System rules: Log system calls made by applications.
            * Filesystem rules: Log access to files and directories
            * Control rules: Rules that modify the auditd behavior.
    
# Network Security

    # Denying Hosts
        - The most basic network security feature you can implement is to use the /etc/hosts/deny file.
        - The TCP Wrappers program on the Linux system reads the hosts.deny file and blocks any attemps from those hosts to access your system.
        - If you want to take a more extreme approach to network security, you can use the /etc/hosts.allow file.
    
    # Disabling Unused Services
        - Many of the legacy network applications use unsecure methods of transferring user data as well as application data.
            - FTP, Telnet, Finger, Mail services
    
    # Changing Default Ports
        - For an application to communicate on a network, it must use a network port. The port is a unique number assigned to the application so that when a remote client communicates with the server, the server knows which application to send the connection to.
        - There are 3 categories:
            * Well-known ports: Ports between 0 and 1023 that have been formally assigned to specify applications by the Internet Assigned Numbers Authority.
            * Registered ports: Ports between 1024 and 49151, which are registered with IANA but not officially assigned.
            * Private ports: Ports greater than 49151, which can be used by any application.
        - Most of the popular network applications have been allocated well-known ports by IANA and are expected to be using those ports. These ports are listed in the /etc/services file on the Linux system.
    
    # Using Encryption on the Network
        - SSH, SCP, SFTP and HTTPS are secure encryption ways.
        - THe Secure Sockets Layer(SSL) protocol, along with the newer Transport Layer Security (TLS) protocol, is commonly used to encrypt data as it traverses the network.
        - The OpenSSL package doesn't provide the actual network applications but is a library that provides the framework required to send and receive encrypted data on the network.
        

                