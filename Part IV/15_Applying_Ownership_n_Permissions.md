# Looking File and Directory Permissions
    - The core security feature of Linux is file and directory permissions.
    - Linux accomplishes that by assigning each file and directory an owner and allowing that owner to set the basic security settings to control access to the file or directory.

    # Understanding Ownership
        - Linux uses a three-tiered approach to protecting files and directories:
            * Owner: Within the Linux system, each file and directory is assigned to a single owner.
            * Group: The Linux system also assigns each file and directory to a single group of users.
            * Others: This category of permissions is assigned to any user account that is not the owner nor in he assigned user group.

                # Changing File or Directory Ownership
                    - The root user account can change the owner assigned to a file or directory by using the chown command.
                        chown [OPTION] newowner filenames
               
                # Changing the File or Directory Group
                    - The file or directory owner, or the root user account, can change the group assigned to the file or directory by using the chgrp command.
                        chgrp [OPTIONS] newgroup filenames
                    - If you're owner of the file, you can only change the group to a group that you belong to.

    # Controlling Access Permissions
        - Linux uses three types of permission controls: 
            * Read: The ability to access the data stored within the file or directory
            * Write: The ability to modify the data stored within the file or directory.
            * Execute: The ability to run the file on the system, or the ability to list the files contained in the directory.
        - You can assign each tier of protection different read, write, and execute permissions. This creates a set of nine different permissions that are assigned to each file and directory on the Linux system. 
        - The first character denotes the object type. A dash indicates a file, whilea d indicates a directory.
        - The next three characters denote the owner permissions in the order of read, write, and execute. A dash indicates the permission is not set, while the r,w, or x indicates the read, write, or execute permission is set. The second set denotes the group permissions and last set assigned to user accounts that are not the owner or a member of the group assigned to the file or directory.
        - In symbolic mode, you denote permissions by using a letter code for the owner(u), group(g), others(o), or all(a) and another letter code for the read(r), write(w), or execute(x) permission. The two coes are separated with a plus sign(+) if you want to add a permission, a minus sign(-) to remove the permission,or an equals sign(=) to set the permission as the only permission.

    # Exploring Special Permissions
        - There are three special permission bits that Linux uses for controlling the advanced behavior of files and directories.
            - The set user ID(SUID) bit is used with executable files. It tells the Linux kernel to run the program with the permissions of the file owner and not the user account actually running the file.
            - The SUID bit is indicated by an s in place of the execute permission letter for the file owner: rwsr-xr-x.
            - To set the SUID bit for a file, in symbolic mode add s to the owner permissions, or in octal mode include a 4 at the start of the octal mode setting:
                - chmod u+s myapp
                - chmod 4750 myapp
        - The set group ID(SGID) also called GUID, for files it tells Linux to run the program file with the file's group permissions. It's indicated by an s in the group execute position.
            - Creates an environment where multiple users can share files. When a directory has SGID bit set, any files users create in the directory are assigned the group of the directory and not that of the user.
            - To set the SGID bit, in symbolic mode add s to the group permissions, or in octal mode include a 2 at the start of the octal mode setting:
        - The sticky bit is used to protect a file from being deleted by those who don't own it, even if they belong to the group that has write permissions to the file.
            - The sticky bit is enoted by a t in the execute bit position for others: rwxrw-r-t. OCtal mode include a 1 at the start of the octal mode setting
    
    # Managing Default Permissions
        - The user mask feature defines the default permissions Linux assigns to the file or directory. The user mask is an octal value that represents the bits to be removed from the octal mode 666 permissions for files or the octal mode 777 permissions for directories.
        - It is set with umask command.
        - The first octal value represents the mask for the SUID(4), GUID(2), and sticky(1) bits assigned to files and directories you create. The next three octal values mask the owner, group, and other permission settings.
        - You can change the default umask setting for your user account by using the umask command from the command line: umask 027
    
    # Access Control Lists
        - You can only assign permissions for a file or directory to a single group or user account. In a complex business environment with different groups of people needing different permissions to files and directories, that doesn't work.
        - ACL( Access Control List) is a more advanced method of file and directory security. The ACL allows you to specify a list of multiple users or groups and the permissions that are assigned to them. 
            * getfacl( allows you to view the ACLs assigned to a file or directory) commands. If you've only assigned basic security permissions to the file, those still appear in the getfacl output.
            * setfacl command allows you to modify the permissions assigned to a file or directory using the -m option or remove specific permissions using the -x option. you define the rule with three formats:
                u[user]:uid:perms
                g[roup]:gid:perms
                o[ther]::perms
                - setfacl [options] rule filenames
    
    # Context-Based Permissions
        - Both the original permissions method and the advanced ACL method of assigning permissions to files and directories are called discretionary access control (DAC) methods.
        - MAC( Mandatory Access control) allow the system administrator to define security based on the context of an object in the Linux system to override permissions set by file and directory owners.
            # SELinux: RHB
                - The Security-Enhanced Linux(SELinux) application implements MAC security by allowing you to set policy rules for controlling access between various types of objects on the Linux system, including users, files, directories, memory, network ports, and processes.
                    
                    # Enabling SELinux
                        - The /etc/selinux/config file controls the basic operations of SELinux. There are two primary settings that you need to set:
                            - SELINUX: This setting determines the operation of SELinux. Set this to enforcing to enable the policy rules on the system and block any unaithorized access.
                                * permissive and disabled
                            - SELINUXTYPE: Determine which policy rules are enforced. The targeted setting is the default and only enforces network daemon policy rules.
                                * minimum and mls and strict.
                        - To change the state of SELinux, you can use the setenforce utility from the command line.
                    
                    # Understanding Security Context
                        - SELinux labels each object on the system with a security context. The security context defines what policies SELinux applies to the object.
                            user:role:type:level
                        - To view the security context assigned to objects, add the -Z option to common Linux commands such as id, ls, ps, and nestat.
                        - The semanage utility allows you to view and set the security context for user accounts on the system. For files and directories, the Linux system sets their security context when they are created, based on the security context of the parent directory.
                        - You can change the default security context assigned to a file by using the chcon or restorecon utilities.
                            chcon -u newuser -r newrole -t newtype filename
                    
                    # Using Policies
                        - SELinux controls access to system objects based on policies. In the targeted security mode, each policy defines what objects within a specific type security context can access objects within another type security context. This is called type enforcemnt.
                        - SELinux maintains policies as text files within the /etc/selinux directory structure.
                        - SELinux uses a method of enabling and disabling individual policies without having to modify a policy file.
            
            # AppArmor: Debian
                - It controls the fles and network ports applications have access to.
                - AppArmor also defines access based on policies but calls them profiles. Profiles are defined for each application inthe /etc/apparmor.d directory structure.
                - Each profile is a text file that defines the files and network ports the application is allowed to communicate with and the access permissions allowed for each.
                - The name of the profile usually referenves the path to the application executable file, replacing the slashes with periods.
                - To determine the status of AppArmor on your Linux system, use the aa-status command.
    
    # Understanding Linux User Types
        # Types of User Accounts
            - There are three basic types of user accounts in Linux:
                # Root:
                    - The root user account is the main administrator user account on the system. It is identified by being assigned the special user ID value of 0.
                    - The root user account has permissions to access all files and directories on the system, regardless of any permission settings assigned.

                # Standard:
                    - Standard Linux user accounts are used to log into the system and perform standard tasks, such as run desktop applications or shell commands.
                    - Standard Linux users normally are assigned a $HOME directory, with permissions to store files and create subdirectories.
                    - They can't access files outside of their $HOME directory unless given permission by the file or directory owner.
                
                # Service
                    - Service Linux user accounts are used for applications that start in the background, such as network service like the Apache web server or MySQL database server. 
                    - By setting the password value in the shadow file to an asterisk, these user accounts are restricted so that they cannot be used to log into the system.
                    - The login shell defined in the /etc/passwd file is set to the nologin value to prevent access to a command shell.

        # Escalating Privileges
            - Most Linux administrators use privilege escalation to allow their standard Linux user account to run programs with the root administrator privileges.
                - su: The su command is short for substitute user. It allows a standard user account to run commands as another user account, including the root user account.
                - sudo: The sudo command is short for substitute user do. It allows a standard user account to run any command as another user account, including the root user account.
                - sudoedit: The sudoedit command allows a standard user to open a file in a text editor with privileges of another user account, including the root user account. The sudoedit command also prompt the user for their own password to validate who they are.
             
            The sudoers file contains not only a list of user accounts but also groups whose users are allowed administrator privileges. There are two common user groups that are used for these privileges:
                * sudo for Debian-based distributions use the sudo group
                * wheel for Red Hat-based distributions.
            
        # Restricting Users and Files
            - There are two commands that you should know about that don't really have anything to do with file ownership or permissions but instead are related to user and file restrictions.
                - The ulimit command helps you restrict access to system resources for each user account. 
                    - As a user account consumes system resources, it places a load on the system, but in CPU time and memory.
                    - If you're working in a multiuser Linux environment, you may need to place restrictions on how many resources each user account can consume.
                    - That's where the ulimit command comes in.
                - The chattr command modifies the attributes assigned to a file or directory. The format of the chattr command is
                    chattr [ mode ] files...
                        * The mode option defines what attributes to set or unset.
                        


