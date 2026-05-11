- Authentication is defined as determining if a person or program is who they claim to be.

# Managing User Accounts
    # Adding Accounts
        - To add a new user account on the system, the useradd utility is typically used. 
        - /etc/skel & /home/userid directories may not be used depending upon the other configuration.
            
            # The /etc/login.defs File 
                - It contains directives for use in various shadow password suite commands. Shadow password suite is an umbrella term for commands dealing with account credentials, such as the useradd, userdel, and passwd commands.
                - A user identification number(UID) is the number used by Linux to identify user accounts. A user account, sometimes called a normal account, is any account an authorized human has been given to access the system, with the appropriate credentials, and perform daily tasks.
                - System accounts are accounts that provide services(daemons) or perform special tasks on a local server, such as the root user account. A system account's minimum UID is set by the SYS_UID_MIN, and its maximum is set by the SYS_UID_MAX directive.
                - The /etc/login.defs file is only one of the configuration files used for the user account proccess's creation side.
            
            # The /etc/default/useradd File
                - The /etc/default/useradd file is another configuration file that directs the process of creating accounts.
                - notice the HOME directive(In Listening 10.3) is set to  /home, which means that any newly created user accounts will have their account directories located within the /home directory.
                - If CREATE_HOME is not set to no within the /etc/login.defs file, a home directory is not created by default.
                - cat /etc/default/useradd or useradd -D to view the config file.
                - The SHELL directive is set to /bin/bash, which means when you access the command line, your user process is running the /bin/bash shell program.
                    - Some distribution such as Ubuntu, set the SHELL directive by default to /bin/sh, which is a symbolic link to another shell.
            
            # The /etc/skel/ Directory
                - The /etc/skel directory, or the skeleton directory as it is commonly called, holds files.
                - If a home directory is created for a user, these files are to be copied to the user account's home directory when the account is created.
                - The /etc/skel files are copied to user account home directories only when the account is created. Therefore, if you make changes to the files later, you'll have to migrrate those changed files to current user accounts either by hand or by shell scripts.
            
            # The /etc/passwd File
                - Account information is stored in the /etc/passwd file. 
                - Each account's data occupies a single line in the file. When an account is created, a new record for that account is added to the /etc/passwd file.
                - The /etc/passwd records contains contain seven field separated by a delimiter.
                - The seven field may contain /sbin.nologin or /bin/false default shell, this prevent an account from interactively logging into the system. /sbin/nologin is typically set for system service account records.
                - System service ( daemons) do need to have system accounts, but they do not interactively log in.
                    - /sbin/nologin displays a brief message and logs you off, before you reach a command prompt, if you malicously attempt log in.
                    - /bin/false logs you off with no messages.
            
            # The /etc/shadow File
                - Another file that is updated when an account is created is the /etc/shadow file.
                - It contains information regarding the account's password, even if you have not yet provided a password for the account.
                - There are nine fields in total, described in the /etc/shadow records file.
                
            # The Account Creation Process
                - Distributions tend to vary greatly in their configuration when it comes to user accounts. Therfore, before you launch into creating accounts with useradd utility.
                - The useradd command, is the primary tool for creating user accounts on most distributions.
                - In Rocky Linux distribuiton the home directory will be created by default, because CREATE_HOME is set to yes. In Ubuntu CREATE_HOME is not set, so it will default to no.
                - When creating a user account on a home directory and used the bash shell, you will need to employ additional useradd command options.
                - Another way to view account records in the /etc/passwd and /etc/shadow files is via the getent utility.
                - When creating an account, you can create a password via the crypt utility and then add it when the account is created via the -p option on the useradd utility.
            
            # Maintaining Passwords
                - Wheb you first create an interactive account, you should immediately afterward create a password for that account using the passwd utility.
                - To update a password for a particular user using the passwd utility and pass the user's account name just enter passwd.
                - YOu can do more than set and modify passwords with the passwd utility, per the options available which requires super user privileges.
                - the chage program can modify password settings.
            
            # Modifying Accounts
                - The utility employed to modify accounts is the usermod program.
                - You can make many modifications to user accounts via the usermod utility's switches and has the commonly used options.
                
            # Deleting Accounts
                - The userdel utility is the key tool in this task. The most common option to use is the -r switch. This option will delete the account's home directory tree and any files within it.
            
            # Managing Groups
                - Groups are organizational structures that are part fo Linux's discretionary access control (DAC).
                - DAC is the traditional Linux security control, where access to a file, or any object, is based on the user's identity and current group membership.
                - Groups are identified by their name as well as their group identification number (GID).
                - The fourth field in the record is the account's GID, which is the default group.
                - Once a new group is created, you can set group membership, which is simply adding user accounts to the group.
                - If you need to modify a group, the groupmod command is helpful.
                - To remove a group, the groupdel utility is employed.

            # Setting Up the Environment
                - After a user authenticates with the Linux system and prior to reaching the Bash shell's command-line prompt, the user environment is configured.
                - The user environment configuration is accomplished via environment files, these files contain Bash shell commands to perform the necessary operations and are covered in this section along with a few environment variable highlights.

                # Perusing Bash Parameters
                    - The Bash shell uses a feature called environment variables to store information about the shell session and the working environment.
                    - set,env, and printenv command to view all the various environment variables set on your system.
                    - When you start a Bash shell by logging into the Linux system, by default Bash checks several files for the configuration, these files are called environmet files(startup files).
                    - You ca start Bash shell in three ways:
                        * As a default login shell, such as when logging into the system at a tty# terminal.
                        * As an interactive shell that is started by spawning a subshell, such as when opening a terminal emulator in a Linux GUI.
                        * As a noninteractive shell(also called non-login shell) that is started, such as when running a shell script.
                
                # Understanding User Entries
                    - There are 4 potential files found in the user's home directory, $HOME, that are environmental files. For a default login or interactive shell, the first file found in the following order is run and, the rest are ignored.
                        * .bash_profile
                        * .bash_login
                        * .profile
                        * .bashrc is run from the file founf in the preceding list, anytime a noninteractive shell is started the .bashrc file is run.
                        - To modify your shell's primary prompt($PS1) persistently, you can do so via adding the modification to one of your local environment configuration files.
                        - Individual user environment files are typically populated from the /etc/skel/ directory, depending o your account creation configuration settings.

                    # Grasping Global Entries
                        - Global configuration files modify the working environment and shell sessions for all users tarting a Bash shell. These can be modified by the account user via adding user entries into their $HOME environment fies.
                        -  The global environment files consist of the following:
                            * the /etc/profile file
                            * File within the /etc/profile.d/ directory
                            * The /etc/bashrc or the /etc/bash.bashrc file
                        - Instead of changing the /etc/profile or other file for global environment needs, you create a custom environment file, give it the .sh file extension, and place it in the /etc/profile.d/ directory.
                
                # Querying Users
                    # Exploring the whoami Utility
                        - The 'whami' command will display what user account you are currently using. 
                    
                    # Understandingthe who Utility
                        - The 'who' command provides a little more data than the whoami utility.
                        - when used by itself it shows all the current system users, the terminal they are using, the data and time they entered the system, and i casesof remote users, their remote IP address.
                        - The 'w' command provides a great deal of useful information.

                    # Identifying with the id Program
                        - The 'id' utility allows you to pull out various data concerning the current user process.
                    
                    # Displaying Access History with the last Utility
                        - The 'last' command pulls information from the /var/log/wtmp file and displays a list of accounts showing the last time they loged in/out of the system or if they are still logged on.
                        - Be aware that the /var/log/wtmp file typically get automatically rotated via the cron utility.
                
                # Managing Disk Space Usage
                    - One way to prevent a filesystem from filling up with files and causing program or entire system issues is to set limits on users' disk space usage. This is accomplished via quotas.
                    - There are 4 steps for enabling quotas on a particular filesystem. 
                        * Modify the /etc/fstab file to enable filesystem quota support.
                        * If the file system is already mounted, unmount and remount it. If the filesystem was not previously mounted, then just mount it.
                        * Create the quotas files.
                        * Establish user or group quota limits and grace periods.
                    - You can create the quota files needed to enforce limits. This is done via the quotacheck utility. 
                        * the -c creates te needed file.
                        * -u creates the aquota.user file, and the -g creates the aquota.group file.
                    - You can create limit using 'edquota' utility. -u to edit user quota, and -g to edit group quota.
                    - 'block' and 'inodes' are preset items you cannot permanently modify, because they were obtained when quotacheck was previously run. but you can modifgy their soft and hard link for both of them.
                        * Hard link no grace period.
                        * soft link has a grace period set up in group.