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
                - There are several simple commands you can use with the systemctl utility to manage systemd services and view information regarding them.
                    * systemctl COMMAND UNIT-NAME
                            - daeon-reload,disable, edit, enable, mask, restart, start, status, stop, reload, umask
                - The sytemctl program is a handy tool to use when troubleshooting systemd issue, such as unit name resolution problems and services not starting action.
        
        # Examining Special Systemd Commands
            - systemd can manage what targets( groups of services) are started at system boot time, jump between various system states, and even analyze your system's boot time performance. example is: systemctl is-system-running command. 
                THe various status provided: running, degraded, maintenance, initializingm starting, stopping.
            - Other useful systemctl utility commands deal with obtaining, settingm and jumping the system's target. 
                * get-default: This displays the system's default target. you can set it with super user privileges through systemctl set-target command.
                * set-default:
                * isolate: It is handy for jumping between system targets. when used along a target name for an argument, all services and processes not enabled in the listed target are stopped.
                    - isolate command can only be used with targets unit file that have AllowIsolate=yes directive set.
                        * Rescue Target: The sytem mount all the local filesystems, only the root user is allowed to log into the system, networking service are turned off, and only a few other services are started.
                        * Emergency Target: The system only mounts the root filesystem, and it mounts it as read-only. it only allows the root user to log into the system, networking services are turned off, and only a few other services are started.
                        - A handy systemd component is the sytemd-analyze utility. with this you can investigate your system's boot performance and check for potential system initialization problems.
        
    # Managing SysV init Systems
        - Systemd is backward compatible with SysV init, so understanding SysV init is important.

        # Understanding Runlevels
            - At system boot time, instead of targets to determine what groups of services to start, SysV init uses runlevels.
            - Setting the default runlevl is the first step in configuring certain services to start at system initialization.
                - Each service must have an initialization script , located typically in the /etc/init.d/ directory. can be viewed with ls -1F /etc/init.d/
            - These initialization scripts are responsible for starting, stopping, restarting, reloading, and displaying the status of various system services.
                * rc scripts(etc/init.d/ or /etc/rc.d/) run the scripts in a particular directory . The directory picked depends on the desired runlevel. Each with its own sub-directory.
            - The rc script goes through and runs all the K(kill) scripts first, passsing a stop argument to each script, then run all the S( start) scripts, passing a start argument to each script.
    
        # Investigating SysV init Commands
            - The various SysV init commands help in starting and stopping services, managing what services are deployed at various runlevels, and jumping between runlevels on an already running Linux system.
                - It uses the telinit or init to do so.
                    init(telinit) DESTINATION-RUNLEVEL
                        Note: runlevel command shows the previous and current runlevel.
            - To view a SysV init managed service's status and control whether or not it is currently running, use the service utility.
                * syntax:
                    service SCRIPT COMMAND [OPTIONS]
                The SCRIPT in the service utilitu refers to a particular service script within the /etc/init.d/ directory. The service utility executes the script, passing it the designated COMMAND.
            - To configure various services to start at different runlevels, there are two different commands you can use. The one you employ depends on which distribution you can use. 
                - The chkconfig utility has several different formats. They allow you to check what runlevels a service will start or not start on. ( Red Hat-based distros)
                    - To enable service at muliple runlevels, you'll need to emply the level options.
                - The update-rc.d utility for Debian has its own set of options and arguments.

    # Digging Deeper into Sytemd
        
        # Looking at Systemd Mount Units
            - Distributions using systemd have additional options for persistently attaching filesystems. filesystem can be specified either within the /etc/fstab file or within a mount unit file.
            - A mount unit file provides configuration information for systemd to mount and control designated filesystems.
            - A mount unit file's content mimic other systemd unit files, with a few special sections and options.
                - Notice that the file has the typical three sections for a unit file.[Unit][Mount][Install]
                    - [Mount], containing directives specific to mount type unit files.
                    - [Instal], set either the wantedby or the requiredby directive to the desired target. If not the server will not mount upon a server boot.
            - To ensure that systemd will mount the filesystem persistently, the mount unit file must be enabled to start at boot, as other systemd units are enabled.
            - Only use mount unit if you need to teak the persistent filesystem configuration.
        
        # Exploring Automount Units
            With systemd, you can also configure on-demand mounting as well as mounting in parallel using automount units.
            - A automount unit file operates similarly to a mount unit file. The naming convention is the same, except that the filenae extension is .automount.
            - Within an automount unit file, for the [Automount] section, only the following three directive are available:
                * Where(required) directive is configured the exact same way as it is in mount unit files. With this directive, you set the mount point.
                * DirectoryMode directive is not a required option. This setting determines the permissions placed on any automatically created mount point and parent directories. default set to 0755.
                * TimeOutIdleSec(not required) directive allows you to set the maximum amount of time( in seconds) a mounted filesystem can be idle. Once the time is reached teh filesystem is unmounted. by default disabled

        # Focusing On Timer Unit Files  
            - Allows you to define events that occur at specific dates or times, similar to how the cron program works. The timer unit files, though, allows you to finetune exactly when a program starts.
                - Designated by a .timer file extension, and include a [Timer] section to define the directives required to determine when to start the event.








D-BCE
ADE-ABCDE
A
C
C-E
BDE-BD
D
B-A
A-E
A-B
E-D
A-CE
C-A
C
BE-ABDE
B
D
A-E
A-C
ACD






