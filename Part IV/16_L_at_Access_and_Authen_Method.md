# Getting to Know PAM
    - Pluggable authentication modules(PAMs) provide centralized authentication services for Linux and appplications. PAM provides authentication libraries that compile into the application, becoming an intermediary between the application requiring authentication and an authentication method.
        * Password: PAM supports using both the /etc/passwd and /etc/shadow password files to authenticate using a text password.
        * Certificate: PAM can use public key infrastructure(PKI) certificate stores to authenticate users.
        * Lightweight Directory Access Protocol (LDAP): PAM can connect to a centralized LDAP server in an organization to support network logins.
        * Kerberos: PAM supports the Kerberos authentication system, which issues a token to clients when they log into the system.
        * Multifactor authentication (MFA): PAM supports several types of MFA environments, such as biometrics, tokens, public key infrastructure(PKI),and one-time passwords emailed to users.
    - PAM controls that all with configuration files. Programs that need to use PAM services are compiled with the PAM library, libpam.so, and have an associated PAM configuration file.
        Application that uses PAM are "PAM-aware".
    
    # Exploring PAM Configuration Files
        - PAM configuration files are located in the /etc/pam.d/ directory.
        - The records in a PAM configuration file have a specific syntax.
            type contro-flag pam-module [module-options]
            The "type" parameter, sometimes called a context or module interface, designates a particular PAM service type. The 4 PAM service types are;
                - account, auth, password, session
        - The pam-module portion of the /etc/pam.d/ configuraton file record is simply the filename of the module that will be doing the work.
        - A designated pam-module is called in the order it is listed within the PAM configuration file. This is called the module stack. Each pam-module returns a status code, which is handled via the record's control-flag setting.
    
    # Enforcing Strong Passwords
         - These various PAM modules can help to enforce strong password:
            * pam_unix.so
                - This module performs authentication using account and password data stored in the /etc/passwd and /etc/shadow files.
            * pam_pwhistory.so
                - This module checks a user's newly entered password against a history database to prevent a user from reusing an old password. The password history file, /etc/security/opasswd, is locked down.
                - You must modify one of the /etc/pam.d configuration files. Along with specifying the password type and the module name, you can set one or more of the MODULE-OPTIONS.
            * pam_pwquality.so
                - Using pam_pwquality.so, you can enforce rules for new passwords, such as setting a minimum password length. You can configure needed directives within the /etc/security/pwquality.conf file or pass them as module options.
                - There are several password quality directives you can set within the pwquality.conf file.
        
    # Locking Out Accounts
        - A brute-force attack occurs when a malicious user attempts to gain system access via trying differnt passwords over and over again for a particular system account.
        - The pam_tally2.so and pam_faillock.so modules allow you to implement account lockout. The two modules shares three key module options. 
            - The pam_tally2 command allows you to view failed login attempts. Ubuntu
            - It is typically better to use the pam_faillock.so module for Red Hat-based Distro.
                - There are 4 pam_failloc.so module records. Within these recods are a few options and one contol flag that have not yet been covered:
                    * preauth audit, [default=die], authfail, authsucc.
                - You need to modify the password-auth file correctly and add the exact recods as wee added to the file.
                - The faillock command allows you to view failed login attemps.
    
    # Limiting Root Access
        - If properly configured, the pam_securetty.so PAM module and the /etc/securetty file are used to restrict root account logins.
        - To understand the /etc/securetty file records, you need to understand how TTY terminals are represented. When you log into a virtual console, typically reached by Crtl+Alt+Fn Key sequence.
        - When you log into the system via its graphical interface, a who or w command's output will show something similar to :0. 
        - If you open a terminal emulator pogram, you are opening a TTY terminal. called a pseudo-TTY, thatis represented by /dev/pts/* file.

# Exploring PKI Concepts
    - The primary purpose of cryptography is to encode data in order to hide it or keep it private. Here plaintext is turn into to ciphertext via cryptographic algorithms this is called encryption.
    - Converting it back to plaintext is decryption.

    # Getting Certificates
       - A few members of the PKI team are the certificate authority (CA) structure and CA-issued digital certificates.
            - After verifying a person's identity, a CA issues a digital certificate to the requesting person.
            - The digital certificate provides identification proof along with an embedded key, which now belongs to the requester.
            - The certificate holder can now use the certificate's key to encrypt data and sign it using the certificate.
        

    # Discovering Key Concepts
        - It is critical to understand cipher keys and their role in the encryption/decryption process. It comes in two flavors - private and public/private.
            # Private Keys( Symmetric keys) called private or secret keys, encrypt data using a cryptographic algorithm and a single key.
                - They are typically fast, but to decrypt the data you need to share the private key.
            # Public/Private Key Pairs Asymmetric keys, also called public/private key pairs, encrypt data using a cryptographic algorithm and two keys.
                - The public key is use to encrypt the data and the private key is use to decrypt it.
                - The public key is meant to be shared, while the private key can be protected with a passphrase.
    
    # Securing Data
        - Hashing uses a one-way mathematical algorithm that turns plaintext into a fixed-length ciphertext.
        - Hashing can be use in data comparison, if two file has the same message digest then they have the same data.
        - The hash can be protected by adding salt, which is adding random data along with the input file. A salted hash is used in the /etc/shadow file to protect passwords.
        - A keyed message digest is created using the plaintext file along with a private key.
    
    # Signing Transmissions
        - Another practical implementation of hashing is in digital signatures, which is a cryptographic token that provides authentication and data verification.
        - It is a message digest of the original plaintext data, which is then encrypted with a user's private key and sent along with the ciphertext.

# Using SSH
    - When you connect over a network to a remote server, if it is not via encrypted method, network sniffers can view the data being sent and received.
    - Secure Shell (SSH) has resolved this problem by providing an encrypted means for communication.

    # Exploring Basic SSH Concepts
        - To create a secure OpenSSH connection between two systems, use the ssh command.
            ssh [OPTION] username@hostname
        - For a successful encrypted connection, both systems ( client and remote) must have the OpenSSH installed and the sshd daemon running.
        - The OpenSSH application keeps track of any previously connected hosts in the ~/.ssh/known_hosts file. This data contains the remote servers' public keys.
        - The rsync utility can employ SSH to quickly copy files to a remote system over an encrypted tunnel. To use OpenSSH with the rsync command, add the username@hostname before the destination file's location.
        - You can also use the ssh command to send commands to a remote system. Just add the command, between quotation marks, to the ssh command's end.
    
    # Configuring SSH
        - Ensuring that your encrypted connection is properly configured is critical for securing remote system communications.
        - If you need to make SSH configuration changes, it is essential to know which configuration file(s) to modify.
            - For an individual user's connections to a remote system, create and/or modify the client side's ~/.ssh/config file.
            - For every user's connection to a remote system, create and modify the client side's /etc/ssh/ssh_config file.
            - For incoming SSH connection requests, modify the /etc/ssh/sshd_config on the server side.
        - There are several OpenSSH configuration directives. You can peruse them all via the man pages for the ssh_config and sshd_config files. However, there are a few vital directives for the sshd_config file:
            - AllowTcpForwarding, ForwardX11, PermitRootLogin, Port.
    
    # Generating SSH Kwys
        - Typically, OpenSSH will search for its system's public/private key pairs. If they are not found, OpenSSH automatically generates them. These key pairs, also called host keys, are stored in the /etc/ssh/ directory within files.
        - The public key files end in the .pub filename extension, the standard filename:
            ssh_host_KeyType_key
        - They key filename's KeyType corresponds to the digital signature algorithm used in the key's creation. The different types you may see on your system are as follows:
            - dsa, rsa, ecdsa, ed25519
        - There may be times you need to manually generate these keys or create new ones, the ssh-keygen utility is employed.
        
    # Authenticating with SSH Keys
        - Entering the password for every command employing SSH can be tiresome. However, you can use the keys instead of a password to authenticate. A few steps are needed to set up this authentication method:
            - Log into the SSH client system.
            - Generate an SSH ID key pair, via ssh-keygen( you must design the correct key pair filename, which is id_type, where Type is dsa,rsa, or ecdsa)
            - Securely transfer the public SSH ID key to the SSH server computer
            - Log into the SSH server system.
            - Add the public SSH ID key to the ~/.ssh/authorized_keys file on the server system. The ssh-copy-id utility allows you to do this. Not only does it copy over the public key, it also stores it in the server system's ~/.ssh/authorized_keys file for you.
            - Now that the public ID key has been copied over to the SSH server system, the ssh command can be used to connect from the client system to the server system with no need to enter a password.
        
    # Authenticating with the Authentication Agent
        - Using the agent, you only need to enter your password to initiate the connection. After that, the agent remembers the password during the agent session.
            - Log into the SSH client system.
            - Generate an SSH ID key pair and set up a passphrase.
            - Securely transfer the public SSH ID key to the SSH server computer.
            - Log into the SSH server system.
            - Add the public SSH ID key to the ~/.ssh/authorized_keys file on the server system.
            - Start an agent session
            - Add the SSH ID key to the agent session.
        - Step 1 to 5 are nearly the same steps performed for setting up authenticating with SSH ID keys instead of a password.
        - One exception to note is that a passphrase must be created when generating the SSH ID key pair for use with an agent.
    
    # Using SSH Securely
        - There are few things you can do to enhance SSH's security on your systems:
            - Using a different port for SSH than the default port 22:
                - You change this port by modifying the Port directive in the /etc/ssh/sshd_config file to another port number.
            - Disable root logins via SSH:
                - By default it is permissible. To disable root login via SSH, edit the /etc/ssh/sshd_config file. Set the PermitRootLogin directive to no, and either restart the OpenSSH service or reload its configuration file.
            - Manage TCP Wrappers:
                - If a server can employ TCP wrappers, it will have the libwrap library compiled with it. You can check for support by using the ldd command.
                - TCP Wrappers employ two files to determine who can access a particular service. These files are /etc/hosts.allow ( Allows access to designated service) and /etc/hosts.deny ( commonly blocks acccess).
                - These files have simple record syntax:
                    service: IPaddress...
                The search order of these files is critical. For an incoming service request, the following takes place:
                    - The hosts.allow file is checked for the remote IP address.
                        - If found, access is allowed, and no further checks are made.
                    - The hosts.deny file is checked for the remote IP address.
                        - If found, access is denied
                        - If not found, access is allowed.
                        