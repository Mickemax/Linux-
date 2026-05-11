# Troubleshooting Access
    - If a user is having trouble accessing their desired applications, a mixed bag of authentication issues can be the cause.

    # Local
        - Local access refers to those users who are using directly connected interface to the server. These are typically server administrators but may be application users as well.
        - Begin troubleshooting by gathering some basic information:
            # Checking a Newly Created User Account
                - If the account is a newly created account, confirm that it was properly built.
                - New Sysadmins often create user accounts with the useradd command but forget to add its password with the passwd utility.
                - Use either the grep or the getent command to check the /etc/passwd and /etc/shadow file records.
                - If an exclamation mark is present then the password was not created.
            
            # Checking Account Accesses
                - Look at the last time the account was successfully accessed.
                - The lastlog utility searches through the /var/log/lastlog file for users who have logged into the system, but it only maintains the most recent login.
                - The last command searches the /var/log/wtmp for users who have logged in/out and keeps records for the most recent logins and beyond.
                - You can also search lastb command, which search for unsuccessful login attempts.
            
            # Checking Privilege Elevation issues
                - Most Linux distributions permit the use of the sudo command to allow users to perform administrative tasks as the root user account, an approach called privilege elevation.
                - If there a user account not allowed to use the sudo command, check this;
                    - First, take a look at the /etc/sudoers file to see what users and groups are allowed to elevate their privileges.
                    - If the user account isn't specified directly in the /etc/sudoers file, there may be some groups that are specified.
                    - The next step is to see what groups the user account belongs to. The easiest way to do that is by using the id command.
            
            # Checking GUI Issues
                - If you find that the account successfully logged into the system in the past and has no recent failed attemps, find out the user's local access method.
                - If the GUI is being used, have the user attempt to log into a text-based terminal, such as the tty2 terminal.
                - If the user cannot successfully log into a terminal, then something else is amiss.
                - If it can successfully log into a text-based terminal but not the GUI, you've narrowed down the problem. Determine what services are running.
                    - For older SysVinit systems, the runlevel command will show if the graphical environment is current.
                    - For systemd systems, use the command; sudo systemctl status graphical.target
                
            # Checking Terminal Issues
                - If the user typically logs into a text-based terminal and cannot, have them log into a different terminal, either as a different virtual terminal or a graphical desktop.
                - If the login is successful, then look at the original terminal's device file to determine if it is corrupted, using the ls -l command.
                - If the user attempts to log into a different text-based terminal and canot, check to see if getty services are running.
                - These services provide the login prompts for the text-based terminals.
                - The getty.target is active, so getty services are available.
            
            # Checking Additional Local issues
                - Determine if the account is locked. You can employ the passwd -S or the getent command to check this.
                        sudo passwd -S KJaneway
                        sudo getent shadow KJaneway
                - To unlock the account, if desired, use super user privileges and the usermod -U or the passwd -u command.
                - Account expiration dates are typically set up for temporary account users, such as contractors or interns.
                - Notice that this account's expiration date has passed. Therefore the JArcher account is now expired and the user cannot log into it.
                - If this was a mistake or you need to modify it, use super user privileges and the chage -E command to set a new expiration date for the account.
            
    # Remote
        - For remote problem first check that the system is accessible over the network. If the system is accessible, determine how the user is attempting to access the system.
        - If the user is employing OpenSSH, first confirm that the OpenSSH server is running on the system and the firewall is properly configured to allow access.
        - Next review the sshd_config configuration file, the AllowUsers and AllowGroups directives restrict access. Ensure that these are correctly set.
        - Determine if authentication through OpenSSH is via a username and password or via a token.
            * If it is a username/password check that PasswordAuthentication is set to yes.
            * If the OpenSSH authentication is token based, ensure that the private key was properly copied over to the server from the remote system.
        
    # Authentication
        - Layered authentication software could be at the problem's heart. One place to check is the PAM.
        - Look through the PAM configuration files, such as /etc/pam.d/sshd, to ensure that directives are properly set.
        - Also employ the pam_tally2 or faillock utility to check if the user's account is locked due to too many failed login attempts.
        - Does your system employ other authentication products, check their configuration files.
        - Don't forget to check your Linux kernel security module, such as SELinux or AppArmor.
        - While the purpose of these modules is to protect the system from attackers, sometimes policy violations can lock out legitimate users.
            * For SELinux, check the audit log file using the sealart command. Notice that no SELinux policy violations were logged.
            * For authentication issues, peruse these various log files as well:
                - /var/log/auth.log(Debian)
                - /var/log/secure(Red Hat-based)

# Examining File Obstacles
    
    # File Permissions
        /*You're editing a configuration file using the vim editor, but when you try to save the file, you get an error message. Problems like this are directly linked to file permissions*/
        - First use ls -l command to view a file's permission settings and ownerships. Note the file's owner and group. Then determine the permissions of the owner, group, and everyone else.
        - If a problem occurs try to access the file, determine the user's username and groupmemberships using te id command.
    
    # Directory Permissions
        - While the directory permission settings look very similar to file permissions, their effect is different.
        - If youb have a directory shared among users and they are able to delete each other's files but that is not desired, employ the sticky bit on the directory.(covered in 15)
    
    # Working with Advanced Permissions
        - Access control lists(ACLs) allow you to specify permissions for multiple users or groups besides the standard owner, group, and others set.
        - If your Linux system uses ACLs, always check the getfacl utility for additional ACL permissions applied to a file or directory:
        - Besides ACL permissions, Linux systems may employ context-based permissions using either SELinux or AppArmor.
        - To determine if SELinux is active on your Linux system, use the sestatus command.
        - You can change the security context for a file by using the chcon command.
        - SELinux controls access to objects using policies. The getsebool command allows you to list the policies and determine if they're active or disabled and the setsebool command to activate or deactivate them.
        - To determine if AppArmor is active on your system, use the aa-status utility:
            * AppArmor uses profiles to set context permissions. While this output has been truncated, in the actual aa-status output you'll see lots of information about the profiles loaded in the enforce, complain, and commands to change profile settings to accommodate your permission requirements.
    
    # File Creation
        - A user goes to create a file and permission is denied. First check the directory permissions. If all is well there, consider the following items:
            * Are quotas enforced on this partition?
            * Has the disk run out of space?
            * Has the partition run out of inodes?
            * What is the user's umask setting ?
        - If a file cannot be deleted or renamed, check the file's attributes via the lsattr filename command.
        - Just as with access issues, check your Linux kernel security module in situations where a user cannot create or delete files. Peruse the appropriate policy violation log files using the appropriate tools.
        - After you have found the policy violation concerning the file or directory in question, determine if the file/directory was mislabeled, the policy is incorrect, or possibly the wrong security context was used.
    
# Exploring Environment and Shell Issues
    - When dealing with user problems, a potential issue is the user account's default shell. 
    - Check it using the getent command.
    - Notice that instead of the /bin/bash shell as the default shell, the /bin/sh shell is used. On this system, the /bin/sh file is linked to the /bin/dash shell.
    - If this is not desired, you can change the user's default shell via the usermod command.
    - Incorrect or improperly set environment variables can cause various user difficulties. Review a user's environment files, such as the ~/.profile file. While you're at it, check the system's global environment variable settings using the set, env, or printenv command.
    - Ensure that environment variables are exported so they are availalble in subshells( a subshell may occur when a shell script is executed).
    
