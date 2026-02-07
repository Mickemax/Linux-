<!-- The Shell is a special interactive utility that allows users to run programs, manage files, handle processes, and so on.-->

# Handling Files and Directories
    Files on a Linux system are stored within a single directory structure, called a Virtual directory. 
    - The root is the base directory.

# Viewing and Creating Files
	<!-- Metadata is information that describes and provides additional details about data. -->

		- View file's name and its various metadata: List command----> ls [OPTION]... [FILE]...
					[OPTION] :  - Means there are various options(also called switches) you can add to display different file metadata.
								- The bracket indicates that switches are optional.
					
					[FILE] : - File arguments shows you can add a directory or filename.
		
		- pwd : Priting working directory.
		- ll ( Demonstrated on a rocky distribution): is an alias for ls -l( which display the directory and sub-directory metadata).
			<!--An alias is a short command that represent another-->
		- tree : The output from a tree command creates a tierd structure, showing which files are associated with which directory, making it easy to sort things out.
		- lsof: display all files currently open by specific user, program, or even network connection.
		- touch: create empty files. primary use to update a file's timestamps- access and modification.
		- mkdir: create directories.
					- the -p option allows you to create a parent directory of a subdirectory if not exiting already.
					- the -v tells you that the directory was successfully created.
		Note: Uses path reference to create a directory/file in a subdirectory of you current directory.
		
		- cd: change directory.

# Copying and Moving Files	
	- cp: copy a file or directory locally.
				cp [OPTION] SOURCE DEST
	- 