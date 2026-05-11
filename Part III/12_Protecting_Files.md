- Protecting data includes creating and managing backups, often called an archive, is a copy of data that can be restored sometime in the future should the data be destroyed or become corrupted.
# Understanding Backup Types
    - There are different classifications for data backups.
        * System image: A system image is a copy of the OS binaries, configuration files, and anything else you need to boot the Linux system.
        * Full: A full backup is a copy of all the data, ignoring its modification date. 
        * Incremental: It makes a copy only of data that has been modified since the last backup operation ( any backup operation type).
        * Differential: It makes a copy of all data that has changed since the last full backup.
        * Snapshot: It is considered a hybrid approach, and it is a slightly different flavor of backups. With a snapshot backup, you can go back to any point in time and do a full system restore from that point.
        * Snapshot clone: A snapshot is created, such as an LVM snapshot, it is copied, or cloned. Usualy useful in high data I/O because the clone backup takes place on the snapshot and not on the original data.
    - Always periodically test your backups to nesure they really can be restored.
    - Backing up database files can be tricky, as usually there are multiple files involved, and restoring from an incremental backup won't work.
    - With the popularity of ransomware, these days it's become crucial to keep an offline copy of your backup files, keeping them safe from attack.

# Looking at Compression Methods
    - gzip: * To compress a file simply type gzip followed by the file's name. To reverse type gunzip.
            * zcat and zless to list the file in the archive, and zgrep to search for files in the archive.
    - bzip2: * The bzip2 utility offers higher compression rates than gzip but takes slightly longer to perform the data compression.
    - xz: It boasts a higher default compression rate than bzip2 and gzip via the LZMA2 compression algorithm.
    - zip: It operates on multiples files. zip creates a copy of the original file(s).
    - 7-zip: It uses the 7z archive format, which touts a higher compression rate tha most other compression utilities.
             The command line is called 7za.

# Comparing Archive and Restore Utilties
    - There are several programs you can employ for managing backups. Some of the more popular products are Amanda, Bacula, Bareos, Duplicity and BackupPC.
    - Yet, often these GUI and/or web-based programs have command-line utilities at their core.
        -cpio, dd, rsync, tar
    
    # Copying with cpio
        - The cpio utility's name stands for "copy in and out". It gathers together file copies and stores them in an archive file.
        - To create an archve using the cpio utility, you have to generate a list of files and then pipe them into the command.
        - The cpio utility maintains each file's absolute directory reference. To restore files from an archive, employ just the -ivI option.
    
    # Archiving with tar
        - The tar utility's name stands for tape archiver, and it is popular for creating data backups. As with cpio, with the tar command, the selected files are copied and stored in a single file called a tar archive file.
        - It is considered good form to se the .tar extension and tach on an indicator showing the compression method that was used. However, you can shorten it to .tgz if desired.
        - The .snar file extension indicates that the file is a tarball snapshot file. The snapshot file contains metadata used in association with tar commands for creating full and incremental backups.
    
    # Duplicating with dd
        - The dd utility allows you to back up nearly everything on a disk, including the older MBR partitions some older Linux distributions still employ.
            dd if=input-device of=output-device [OPERANDS]
        - The output-device is either an entire drive or a partition. The input-device is the same. Just make sure that you get the right device for out and the right one for in; otherwise you may unintentionally wipe data.
        - The of and if, are operand that assist in dd operations.
        - The lsblk command is used first. When copying disks via the dd utility, it is prudent to make sure the drives are not mounted anywhere in the virtual directory structure.

    # Replicating with rsync
        - The rsync utility is known for speed. With this program, you can copy files locally or remotely, and it is wonderful for creating backups.
        - The archive option, -a , which directs rsync to perform a backup copy.
        - It is fairly simple to conduct rsync backup locally. The most popular options, -ahv, allow you to back up files to a local location quickly.
    
# Securing Off-site/Off-system Backups
    # Copying Securely via scp
        - The scp utility is geared for quickly transferring files in a noninteractive manner between two systems on a network.
        - It is best used for small files that you need to securely copy on the fly, because if it gets interrupted during its operation, it cannot pick back up where it left off.
    
    # Transferring Securely via sftp
        - The sftp utility will also allow you to transfer file securely across the network. However, it is designed for a more interactive experience.
        - The sftp is used with a username and a remote host's IPv4 address. Once the user account;s correct password is entered, the sftp utility's prompt is shown.
        - Before using the sftp interactive utility, it's helpful to know some of the more common commands.
- The rsync, scp and sftp utilities all provide a means to securely copy files.

# Checking Backup Integrity
    - Securely transferring your archives is not enough. You need to consider the possibility that the archives could become corrupted during transfer.

    # Digesting an MD5 Algorithm
        - The md5sum utility is based on the MD5 message-digest algorithm. It was originally created to be used in cryptography.
        - the md5sum produces a 128-bit hash value. You can see from the results in the two listings that the hash values match. This indicates no file corruption occurred during its transfer.
    
    # Securing Hash Algorithms
        - The Secure Hash Algorithms(SHA) is a family of various hash functions. Though typically used for cryptography purposes, they can also be used to verify an archive file's integrity.
        - Each utility includes the SHA message digest it employs within its name.
        - The sha512sum utility uses the SHA-512 algorithm, which is the best to use for security purposes and is typically employed to hash salted passwords in the /etc/shadow file on Linux.
        
    

