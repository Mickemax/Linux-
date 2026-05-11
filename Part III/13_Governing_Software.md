 - A Linux system is only as good as the software you install on it.
 - The Linux kernel by itself is pretty boring you need applications such as web servers, database servers, browsers, and word processing tools to actually do anything useful with your Linux system.

# Working with Source Code
 - The "source" part of the open source world refers to the availability of the actual programming code used to create applications.
    
    # Downloading Source Code
        - While you can use a graphical browser to connect to a website and download source code, that's not always available especially in Linux server environments. 
        - The 'wget' application is a command-line tool from the GNU project that allows you to retrieve files from remote servers using FTP, FTPS. HTTP or HTTPS.
            wget hhtp://remotehost/filename
        - Another one is the 'cURL' application which supports more protocols such as DAP, DICT, FILE, Gopher, IMAP, LDAP, POP3, RTSP, SCP, SFTP, SMTP, and TFTP.

    # Bundling Source Code Packages
        - Source code projects often comprise many different files:
            * Source code files
            * Header files
            * Library files
            * Documentation files
        - The tar program comes in handy for bundling project files to distribute on the internet.
        - For most bundling operations, three basic option groups are commonly used for the tar command:
            -cvf: Create a new tar file
            -tvf: Display the cotents of a tar file
            -xvf: Extract the contents of a tar file
    
    # Compiling Source Code
        - Once you have the source code package files downloaded onto your Linux system, you'll need to compile them to create an executable file to run the application.
        Linux supports a wide variety of programming languages, so you'll need to know just what programming language the application was written in. ONce you know that, you'll need to install a compiler for the program code.
        - the most common tool is GNU Compiler Collection (gcc).
        - Most large applications require additional header and library files besides the source code files to build the final application file.
        - The 'make' utility allows developers to create scripts that guide the compiling and installation process of application source code packages so that even novices can compile and install an application from source code.
    
    # Packaging Applications
        - While the tar, gcc, and make programs make it easier to distribute, compile, and install application source code, that's still somewhat of a messy process for installing new applications.
        - a package is a system for bundling already compiled applications for distribution.
        - Tracking software packages on a Linux system is called pacakge management. Linux implements package management by using a database to track the installed packages on the system.
        - As you would expect, different Linux distributions have created different package management systems for working with their package management databases. Each package management systems uses a different method of tracking application packages and files, but they both track similar information:
            - Application files: The package database track each individual file as well as the folder where it's located.
            - Library dependencies: The package database tracks what library files are required for each application and can warn you if a dependent library file is not present when you install a package.
            - Application version: The package database tracks version numbers of applications so that you know when an updated version of the application is available.
        
        # Installing and Managing Packages
            # Debian Package Tools
                - Debian bundles application files into a single .deb files is the dbkg program.
                - The dbkg program is a command-line utility that has options to install, update, and remove .deb packages files on your Linux system.
                    dbkg [Options] action package-file
                - The action parameter defines the action to be taken on the file.
                - Each action has a set of options that you can use to modify the basic behavior of the action, such as to force overwriting an already installed package or ignore any dependency errors.
                - The dpkg tools gives you direct access to the package management system, making it easier to install applications on your Debian-based system.
            
            # Red Hat Pacakage Tools
                - The Red Hat Linux distribution, along with other Red Hat-based distribution such as Fedora, Rocky, CentOS, use the .rpm package file format.
                - The basic format for the rpm program is as follows:
                    rpm action [options] package-file
                - To use the rpm command, you must have the .rpm package file downloaded ont your system.

        # Understanding Repositories
            - The dpkg and rpm commands are useful tools, but they both have their limitations. If you're looking for new software packages to install, it's up to you to find them. Also if packages are dependent on other it is your job to get the right order.
            - To solve that problem each Linux distribution has its own central clearinghouse of packages, called a repository.
            - Most Linux distributions create and maintain their own repositories of packages.

                # Debian Repository Tools
                    - The core tool used for working with Debian repositories is the apt suite of tools. This includes the apt-cache program, which provides information about the package database and the apt-get program, which does the work of installing updating, and removing packages.
                    - The apt suite of tools relies on the /etc/apt/sources.list.d/ubuntu.sources file to identify the locations of where to look for repositories.
                    - There are a few useful command options in the apt-cache program for displaying information about packages:
                        * depends, pkgnames, showpkg, stats unmet
                
                # Red Hat Repository Tools
                    - In the past, the core tool used for working with Red Hat repositories has been the yum tool( short for YellowDog Update Manager) This too hsa recently been replaced by the dnf tool, which is an updated version of yum.
                    - Both yum and dnf commands use the /etc/yum.repos.d folder to hold files that list the different repositories it checks for packages.
                    - Each file in the yum.repos.d folder contains information on a repository, such as the URL address of the repository and the location of additional package files within the repository.
                    - dnf is able to group packages for distriution, instead of having to download all of t packages needd for a specifc environment( such as for a web server that uses the Apache, MySQL, and PHP servers), you can download the package group that bundles the packages together.
                
                # Graphical Package Tools
                    - The gnome-software is one tool available in both Ubuntu and Rocky distribution.
                    - It is a graphical front end to the PackageKit tool, which itself is a front end that standardizes the interface to multiple package management tools, including apt and yum.
        
    # Using Application Containers
        - Containers allow you to bundle all of the files required for an application, including any dependencies, into one distribution package.
        - The downside to this method, though, is that any deendencies shared among multiple applications are duplicated for each application.

            # Using Snap Containers
                - Snap is an application container developed by Ubuntu.
                - the snapd application manages the snap packages installed on the system and runs in the background.

            # Using Flatpak Containers
                - The flatpak application container format was created as an independent open source project with no direct ties to any specific Linux distribution.
                - That said, battle lines have already been drawn, with Red Hat-based Linux distributions oriented toward using flatpak instead of Canonical's snap container format.
                - By default Red Hat-based Linux distributions don't configure any repositories for flatpak ( called remotes). The most popular flatpak remote is Flathub.
                - When working with a container you must use its Application ID value and not its name.
            
            # AppImage
        

