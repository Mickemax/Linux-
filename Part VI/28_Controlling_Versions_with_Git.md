# Understanding Version Control
    - A version control system (VCS) provides a common central place to store and merge project files so that you can access the latest project version.
    - It protects the files so that a file is not overwritten by another developer and eliminates any extra communications concerning who is currently modifying it.
    - Distributed version control systems(VCSs) make projects even easier. The developers can perform their work offline, without any concerns as to whether or not they are connected to a network.
    - The development work takes place locally on their own systems until they send a copy of their modified files and VCS metadata to the remote central system.
    - Git is a distributed VCS, which is often employed in agile and continuous softeare development environments. 
        * Working Directory: The working directory is where all the program files are created, modified and reviewed. It is typically a subdirectory within the developer's home directory tree.
        * Staging area: A staging area is called the index. This area is located on the same system as the working directory. Program files in the working directory are registered into the staging area via a Git command.
        * Local Repository: This contains each project file's hsitory. It also employs the .git subdirectory.
        * Remote Repository: THe remote repository is typically a cloud-based location. However, it could also be another server on your local network, depending on your project;s needs.
    -Using Git as your VCS includes the following benefits:
        * Performance: Except for sending/retrieving file to/from the remote repository, Git uses only local files to operate, making it faster to employ.
        * History: Git capture all the files's contents at the moment the file is registered with the index.
        * Accurary: Git employs checksum to protect file integrity.
        * Decentralization: Deelopers can work on the same projectm but they don't have to be the same network or system.
    
# Setting Up YOur Environment
    - The Git utility typically is not installed by default. Thus you'll need to install the git package prior to setting up your Git environment.
    - After you have the git package installed on your system, there are four basic steps to setting up your Git environment for a new project:
        * Create a working directory
        * Initialize he .git/ directory
        * Set up local repository options
        * Establish your remote repository
    - The git init command displays a hint that it's using the default name of master of the branch, then creates the .git/ subdirectory.
    - If this is the first this is the first time you have built a .git/subdirecotory on your system, modify the global Git repository's configuration file to include your username and email address.
    - This git config command lets you perform this task, by including the --global on the git config command, the user.name and user.email data is stored in the global Git configuration file.
    - Git configuration information is stored in the global ~/.gitconfig file and the local repository, which is the working-directory/.git/config configuration file.

# Committing with Git 
    - You can begin employing version control, through this 4 steps:
        * Create or modify the program file(s).
        * Add the file(s) to the staging area(index).
        * Commit the file(s) to the local repository.
        * Push the file(s) to the remote repository.

# Merging Versions
    - A branch is an area within a local repository for a particular project section. By default, Git stores your work in the master branch.
    - You can have multiple branches within a project. You can designate the branch you wish to work on to protect files in another branch from being changed.
    - The asterisk(*) indicates the current working branch, you can view the filenames within a particular branch by employing the git ls-tree command.
    - Now that the branch is switched, development on the new user interface(ST-UI.py) can occur without affecting the master branch. However, Git VCS is still employed.
    - When development (and testing) on the new user interface is completed, the develop branch is merged with the master branch(production). To merge branches, use the git merge branch-name-to-merge command.
    - Merges must be performed from the target branch.
    