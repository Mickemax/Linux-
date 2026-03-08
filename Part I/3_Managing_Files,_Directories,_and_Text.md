<!-- The Shell is a special interactive utility that allows users to run programs, manage files, handle processes, and so on.-->

# Handling Files and Directories
    Files on a Linux system are stored within a single directory structure, called a Virtual directory. 
    - The root is the base directory.

# Viewing and Creating Files
	<!-- Metadata is information that describes and provides additional details about data. -->

		- View file's name and its various metadata: List command----> ls [OPTION]... FILE...
					[OPTION] :  - Means there are various options(also called switches) you can add to display different file metadata.
								- The bracket indicates that switches are optional.
					
					FILE : - File arguments shows you can add a directory or filename.
		
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
	
	- To copy a directory you need to add the -r option. This will enact a recursive copy.
	- mv: move or rename a file and directory.
									mv [OPTION] SOURCE DEST
	- rsync: rsync [OPTION] SOURCE DEST
			* This command is used the quickly copy files either locally or across network, in a secure tunnel through OpenSSH.

# Removing Files
	- rm: delete file
			rm [OPTION] File
				OPTION: The difference between -i and -I is -i request deletion at each step, while  -I it ask once before deleting more than three file or a directory full of files.

	- rmdir: delete empty directory

# Linking Files and Directories
	# Hard link - A file is only deleted if link count reaches 0
		- A hard link is a file or directory that has one index(anode) number but atleast two different file name. 
		- Having a single index number means it is a single data file on the filesystem.
				- Syntax: ln SOURCE HARDLINK
				To unlink a hard link file: unlink linkFile

	# Soft link
		- Soft link provides a pointer to a file that may reside on another filesystem.
		- The two file do not share inode number.
			- Syntax: ln -s SOURCE SOFTLINK
			- readlink -f: to find the final file.
		- Stale link is when a soft link points to a file that was deleted or moved.

# Reading Files
	# Reading Entire Text Files
		-	cat [OPTION] FILE / bat [OPTION] FILE
				Primarily use to join together text files and display them, but can also be use to view entire text files.
		- pr [OPTION] FILE
				Primarily use to format text file for printing.
	
	# Reading Text File Portions
		- grep [ OPTIONS] PATTERN [FILE...]
				When searching for a particular text stringm you use the string for the PATTERN is the string
					- i(option) to remove case sensitive
		- head [OPTION] FILE
				the head command displays the first 10 lines of a text file, but with -n it tells the number of line you should display, also works with negative argument to tell what not to display.
		- tail [OPTION] FILE
				the tail command will show a file's last 10 text lines. Comtrary to head when adding the + attribute it print from that line number downward.
					- f(or -follow) to watch additional messages being added.
	
	# Read Text File Pages
		- more [OPTION] FILE
				The more pager utility displays a text at page level with space to move from one page to another and enter to move one line at a time.
		
		- less [OPTION] FILE
				Permit you to move through a file a page at a time, this pager utility also allows you to move backward.

# Finding Information
	# Viewing File Information
		- file FILE
			File command provide basic information about the file you are not familiar with.

		- stat FILE
			The output from command shows information about the file creation, modificationm or lastly accessed.
	
	# Exploring File Differences
		- diff [OPTION] FILES / sdiff [OPTION] FILES ( more user friendly)
			Perform variation of comparison between two files.
				c: demand changes
				a: addition
				d: deletion
	
	# Using Simple Pinpoint Commands
	<!-- Command that quickly locate files are very useful. They allow you to determine of a particular utility is installed on your system, locate a needed configuration file, find helpful ducimentation, and so on.>
	
		- which FILE
			Shows the full pathname of a shell command passed as an argument.
		
		- whereis FILE
			Locate source code files as well as any man pages.
		
		- locate [OPTION] PATTERN
			search a database called mlocate.db, which locate in the /var/lib/mlocate/ directory to check if file exist.
	
	#Using Intricate Pinpoinr Commands

		- find [PATH..] [OPTION] [EXPRESSION]
			Allows you to locate files based on data, such as ownership,lastly modified, permission set on file.
		
		
		
		
		
		
		C
		B
		A
		E
		E
		D,A
		B
		E
		D
		C
		E
		B
		E
		C
		C
		E
		C-a
		A-d
		B-e
		C
		

