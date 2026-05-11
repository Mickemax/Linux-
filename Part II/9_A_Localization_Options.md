# Understanding Localization
    - Localization is the ability to adapt a Linux system to a specific locale.

    # Character Sets
        - A character set defines a standard code used to interpret and display characters in a language.
            - ASCII: The American Standard Code for Information Interchange (ASCII) uses 7 bits to store characters found in the English language.
            - Unicode: AN international standard that uses a 3-byte code and can represent every character known to be in use in all countries.
            - UTF: The Unicode Transformation Format(UTF), which transforms the long Unicode values into either 1-byte (UTF-8) or 2-byte(UTF-16) simplified codes.
        - Once you have decided on a character set for your Linu system, you'll shown in the following section.

    # Environment Variables
        - Programs that need to determine the locale of the Linux system just need to retrieve the appropriate environment variable to see what character set to use.
        - Linux provide the locale command to help you easily display these environment variables.
        - The output of the local command defines the localization information in this format:
            language_country.character set
        - Each LC_ environment variable itself represents a category of more environment variables that relate to the locale settings.
            - Use -ck option to explore the environment variables contained within a category.

# Setting Your Locale 
    # Installation Locale Decisions
        - When you first install the Linux operating system, one of the prompts available during the installation process is for the default system language.
        - When you select a language from the menu, the linux installation script automatically sets the localization environment variables appropriately for that country and language to include the character set required to represent the required characters.
    
    # Changing Your Locale
        # Manually changing the Environment Variables
            - Change the individual LC_localization environment variables just as you would any other environment variable, by using the export command:
                export LC_MONETARY=en_GB.UTF-8
            - That works well for changing individual settings, but it would be tedious if you wanted to change all the localization settings for the system.
            -LANG environment variable control all of them at once.
                export LANG=en_GB.UTF-8
            - This method changes the localization for your current login session, you will need to add the export command to the .bashrc file in your $HOME folder so it runs each time you log in.

        # The localectl command
            - If you're using a Linux distribution that utilizes the systemd set of utilities, you have the localetl command available which by default display the current localization settings:
                - It shows the keyboard layout mapping as well as the X11 graphical environment layout.
            - The localectl command supports many options, but the most common are to list all o the locales installed on your system with the list-locales option and to change the localization by using the set-locale option.
                localectl set-locale LANG=en_GB.utf8
            
    # Looking at Time
        - Linux handles the time as two parts- the time zone associated with the location of the system and the actual time and date within that time zone.

        # Working with Time Zones
            - Most Debian-based Linux systems define the local time zone in the /etc/timezone file, while most Red Hat-based Linux systems use /etc/localtime.
            - To edit you most link that file to a template file stored in the /usr/share/zoneinfo folder.
            - To change the time zone for a linux system, just link the appropriate time zone template file from the /usr/share/zoneinfo folder to the /etc/timezone or /etc/localtime location.
            - Before you can copy the new time zone file, you'll need to remove the original timezone or localtime file.
        
        # Setting the Time and Date
            # Legacy Commands
                - There are two legacy commands that you should be able to find in all Linux distributions for working with time and date values:
                    - hwclock displays or sets the time as kept on the internal BIOS or UEFI clock on the workstation or server.
                        - It provides access to the hardware clock built into the physical workstation or server that the Linux system runs on.
                    - date displays or sets the date as kept by the Linux system.
                        - It allows you to display the time and date in a multitude of formats in addition to setting the time and/or date.
                        - you can also set the time and date using this format: date MMDDhhmm [[CC]YY][.ss]
            
            # The timedatectl Command
                - You can use the timedatectl command to manage the time and date settings on your system.
                - Provides one-stop shopping to see all of the time information, including the hardware clock, called RTC, the date information, and the time zone information.
                - You can also use the timedatectl command to modify any of those settings as well by using the set-time option:
                    # timedatectl set-time "2024-10-05 08:30:00"
            
            # The Network Time Protocol
                - NTP is keep the time and date synchronized with a centralized time server. Can't alter data and time using other command.
                - Instead, you will need to point your Linux server to an appropriate network time server.
                - There are three common NTP software implementations used in the Linux world:
                    * ntpd: Legacy software that uses the Simple Network Time Protocol(SNTP) to connect to a network time server.
                    * chrony: An improved version of the ntpd software that utilizes security features.
                    * timesyncd: Part of the systemd startup utilities package that provides NTP services.
            
            # Watching System Time
                - The time command displays the amount of time it takes for a program to run on the Linux System:
                - After the normal command output, you'll see three additional lines of information:
                    * real: The elapsed amount of time between the start and end of the program.
                    * user: The amount of user CPU time the program took.
                    * sys: The amount of system CPU time the program took.