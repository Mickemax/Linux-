# Looking at init
    - Service startups are handled by the init progam, located in /etc/, the /bin/, or the /sbin/ directory. It typically has a process ID(PID) of 1.
    - The init program or systemd is the parent process for every service on a Linux system.
        * Systemd or SysV init, first find the init program's location, using the which command. and then use the super user privileges to see if the program is linked to another program: readlink -f 
        * the "ps" utility is used, to allow you to view processes. A proccess is a running program.

# Managing Systemd Systems
    - Systemd permit services to be started when the system boots.

    # Exploring Unit Files
        The easiest way to start exploring a systemd is through the systemd units. A unit defines a service, a group of services, or an action. Each consists of a name, a type, and configuration file. There are 12 different systemd unit types.

            - systemctl [OPIONS...] COMMAND [NAME...]
                * main gateway to manage systemd and system services.
                * You can see a list of various units currently loaded in your Linux system.
                * System services ( daemons) have unit files with the .service extension.
                * Groups of services are started via target unit files. At system startup, the default.target unit is responsible for ensuring that all required and desired services are launched at system initialization.

        # Focusing On Service Unit Files
            - Service unit files contains information such as which environment file to use, when a service must be started, what targets want this service started, and so on.
            - Unit configuration file's directory location is critical because if a file is found in two different directory locations, one will have precedence over the other. The following list shows the directory locations in ascending priority order:
                - /etc/systemd/system/
                - /run/systemd/system/
                - /usr/lib/systemd/system/
            - Use systemctl to see the various service unit files available.
            - Their states are called enablement states and refer to when the service is started. There are at least 12 different enablement states, but you'll commonly see these three:
                - enabled: Service starts at system boot.
                - disabled: Service does not start at system boot.
                - static: Service starts if another unit depends on it. Can also be manually started.
            - To see what directory or directories store a particular systemd unit files, use the the systemctl utility.
                or service unit files, there are three primary configuration sections:
                - [Unit]
                        - Within the service unit configuration file's [unit] section, there are basic directives. A directive is a setting that modifies a configuration, such as the After setting.
                     - Note: 'man -k' to get useful information on systemd and unit configuration files.
                            - explore the service type unit file directives  and more via man systemd.service
                - [ Service]
                        - The Service directives within a unit file set configuration items, which are specific to that service.
                - [Install]
                        - The Install directives within a unit file determine what happens to a particular service if it is enabled( start at system boot) or disabled(does not start at system boot).
        
        # Focusing On Target Unit Files
            For systemd, you need to understand the service unit files as well as the target unit files.
                - The primary purpose of target unit files is to group together various services to start at system boot time.
                - The default target unit file, default.target, is symbolically linked to the target unit file used at system boot.
        
        # Modifying Systems Configuration Files
            - Never modify any unit files in the /liblsystemd/system/ or /usr/lib/systemd/system/ directory.
            - To modify a unit configuration file, copy the file to the /etc/systemd/system/ directory and modify it there.
            - If you have a few additional components, you can extend the configuration. using super user privileges, create a new subdirectory in the /etc/systemd/system/ directory maned service.service-name.d, where service-name is the service's name.
            - After making these modifications, there are a few more needed steps. Find and compare any unit file that overrides another unit file by issuing the system-delta command.
                    - It will display any unit files that are duplicated, extended, redirected, and so on.
            - To have your changes take effect, issue the systemctl daemon-reload command for the service whose unit file you modified or extended. After issue the systemctl restart command to restart command to start or restart the service.
        
        # Looking at systemctl
            - Systemctl is the easiest and fastest utility to manage systemd and system services.
            - There are serveral systemctl commands available for you to manage system services.
                - status; it provides a wealth of information.
        