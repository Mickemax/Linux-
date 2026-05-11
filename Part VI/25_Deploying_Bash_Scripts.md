# The Basics of Shell Scripting
    - Shell scripting allows you to write small programs that automate activities on your Linux system.

    # Running Multiple Commands
        - One exciting feature of the Linux command line is that you can enter multiple commands on the same command line and Linux will process them all.
        - Just place a semicolon between each command you enter: date ; who
    
    # Redirecting Output
        - Anoterh building block shell scripting is the ability to store command output. 
        - Output redirection allows us to redirect the output of a command from the monitor to another device, such as a file.
        - To redirect the output from a command, you use the greater-than symbol(>) after the command and then specify the name of the file that you want to use to capture the redirected output.
    
    # Piping Data
        - Piping allows us to redirect the output to another command. The second command uses the redirected output fromm the first command as input data. This feature comes in handy when using commands that process data, such as the sort command.
        - The piping symbol is the bar(|) synbol.
    
    # THe Shell Script Format
        - Shell script files are plain-text files. TO create a shell script file, you just need to use any text editor that you're comfortable with.
        - KDE-based graphical desktop, you can use the KWrite program, or if you're working from a GNOME-based graphical desktop, you can use the GEdit program.
        - pico and nano editor, there is still one last resort: the vi editor.
        - Once you've chosen your text editor, you're ready to create your shell scripts. The first line in the file usually specifies the Linux shell required to run the script. This is written in somewhat of an odd format:
            #!/bin/bash
        - After you specify the shell, you're ready to start listing the commands in your script. You don't need to enter all of the commands on a single line; Linux allows you to place them on separate lines.
    
    # Running the Shell Script
        - The shell uses a special environment variable called PATH to list directories where it looks for commands. If your local HOME folder is not included in the PATH environment variable list of directories, you can't run the shell script file directly.
        - Instead, you need to use either a relative or an absolute path name to point to the shell script file.
        - You can use the chmod command to add execute permission for the file owner.
            - The u+x option add execute privileges to the owner of the file.

# Advancing Shell Scripting
    
    # Displaying Messages
        - When you string commands together in a shell script file, the output may be somewhat confusing to look at. It would help to be able to customize the output by separating it and adding our own text between the output from each listed command.
    
    # Using Variables
        - Variabls allow you to set aside locations in memory to  temporarily store information and then recall that information later in the script by referencing the variable name.
            # Environment Variables
                - Environment variables track specific system information, such as the name of the system, the name of the user logged into the shell, the user's user ID(UID), the default home directory for the user, and the search path the shell uses to find executable programs.
                - You can display a complete list of environment variable available in your shell by using the set command.
                - The $USER, $UID, and $HOME environment variables are commonly used to display information about the logged-in user.
            
            # User Variables
                - User variables allow you to store your own data within your shell scripts. You assign values to user variables using the equal sign.
                - Spaces must not appear between the variable name, the equal signm and the value.
                - The shell script automatically determines the data type used for the variable value. Variables defined within the shell script are called local variables and are accessible only from within the shell script. Global variables are defined outside of the shell script at the main shell level and are inherited by the script shell environment.
            
    # Command-Line Arguments
        - One of the most versatile features f the shell scripts is the ability to pass data into the script when you run it.
        - One method of passing data into a shell script is to use command-line arguments. Command-line arguments are data you include on the command line when you run the command.
            command argument1 argument2
        - You retrieve the values in your shell script code using special numeric positional variables. Use the variable $1 to retrieve the first command-line argument, $2 the second argument, and so on.
    
    # The Exit Status
        - When a shell script ends, it returns an exit status to the parent shell that launched it. The exit status tells us if the shell script completed successfully or not.
        - Linux provides us with the special $? variable, which holds the exit status value from the last command that executed. To check the exit status of a command, you must view the $? variable immediately after the command ends.

# Writing Script Programs
    # Command Substitution
        - Command substitution allos you to assign the output of a command to a user variable in the shell script. 
        - After the output is stored in a variable, you can use standard Linux string manipulation commands( sort or grep) to manipulate the data before dislaying it.
        - Need to use one of two command substitution formats:
            * Placing backticks(`) around the command.
            * Using the command within the $() function.

# Performing Math
    - To include mathematical expressions in your shell scripts, you use a special format. 
    - This format places the equation within the $[] characters.

    # Logic Statements
        # The If Statement
            if [ condition ]
            then 
                commands
            fi

        # The case Statement
            case variable in
            pattern1) commands1;;
            pattern2 | pattern3) commands2;;
            *) default commands;;
            esac
        
    # Loops 
        # The for Loop
            - The for statement iterates through ever element in a series, such as files in a directory or lines in a text document.
            - The format of the for command is as follows:
                for variable in series ; do
                    commands
                done
        
        # The while Loop
            - Another useful loop statement is the while command. This is its format:
                while [ condition ] ; do 
                    commands
                done
    
    # Text Manipulation 
        - Perhaps one of the most powerful uses of shell scripts is quickly and easily manipulating large amount of data.\
            * Globbing: Allowd you to use wildcard characters to search for multiple files and directories in your scripts.
            * Parameter expansion: By placing braces around a variabe name, such as ${test}, you can use parameter expansion, which allows you to specify a substring value from the variable based on an offset and length.
            * Read: The read utility allows you to read text files line by line to process using standard text manipulation tools.
            * Regular expressions: The use of regular expressions allows you to find and replace specific string within files.
    
    # Creating Functions
        - To define a function, you just need to assign it a unique name, then define the code contained in the function.
            function name{
                commands
            }
        - The second format more closing follows how functions are defined in other programming languages:
            name() {
                commands
            }