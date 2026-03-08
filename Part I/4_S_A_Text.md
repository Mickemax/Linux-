# PROCESSING TEXT FILES
    # Filtering Text
        cut OPTION [FILE]
         - it helps extract small data sections.
                + Text File Records: These are single file line that ends in a newline linefeed.
                 - cat -E : Display every newline feed as $.
                 - cut -z : If your text file records ends in the ASCII character NUL(\0).
                + Text File Records Delimiter: For some options to be used, fields must exist with each within each text file record. these are data that is separated by some delimeter.
                + Text File  Changes: Does not modifies file.
        
        # Basic Regular Expressions ( BRE)
            - It is a pattern template you define for a utility.
            - It uses character such as (.*) for multiple character, (.) for one character.
            - [] to represent a range of character, or multiple character.
            - (^) to find text file records that begin with particular characters.
            - Text file records where particular characters are at the record's end, append ($)
        
        # Extended Regular Expressions(ERE)
        - (|) allows you to sepcify two possible words or character sets to match.

    # Formatting text
        sort [OPTION] [FILE]
            - The sort utility sort a file's data.
            - "uniq" command added on to the sort command remove duplicate or inversely, only show the lines that are duplicates.
                        sort [OPTION] [FILE] | uniq
            - printf FORMAT [ARGUMENT]
                Its entire purpose in life is to format and display text data.
                    example: printf "%s\n" "HELLO WORLD"
    
    # Determinig Word Count
        wc [OPTION] [FILE]
            - gathering statistics on various text files, and to determine counts in a text file. The utility will display the file's number of lines, words, and bytes in that order.
                note configuration file length are always under 150 bytes.

# REDIRECTING INPUT AND OUTPUT
    # Handling Standard Output
        - Linux treats every object as a file; output process, such as displaying a text file on a screen.
        # file descriptor that identifies output from a command or script file is 1. STDOUT( Standard Output).
                <!-- file descriptor are integer that classifies a proccess's open files -->
                - echo [ARGUMENT] 
                    Note: A redirection operator allow you to change the default behavior of where input and output are sent.
                        - ">" redirect output to a a file. It overwrite files.
                        - ">>" appends data to a preexisting file.
    
    # Redirecting Standard Error
        - The file descriptor that identifies a command or script file error is 2. STDERR( Standard Error).
            - the basic redirection operator to send STDERR to a file is "2>".
            - "2>>" to append the file.
            - "&>" to send STDERR and STDOUT to the same file. Note they are both sent to the terminal(/dev/tty).
            - Redirect STDERR on garbage(/dev/null).
                    -/dev/null is also called a black hole, anything you put inside cannot be retrieve.
            
    # Regulating Standard Input
        - file regulator that indentifies an input into a command or script file is 0.STDIN(Standard Input).
            - "<" redirect STDIN from specific file into command.
                - tr command change the value of an input to another.
            - "<>" Redirect STDIN from specified file into command and redirect STDOUT to specific file.
            
    # Piping Commands
        - Using the vertical bar to operate more than one command at a time.
            command 1 | command 2 [| command n]...
                The syntax for pipe redirect shows that the first command, command1, is executed. Its STDOUT is redirected as STDIN into the second command, command2.
            
            tee [OPTION] [FILE]
                - This command safe the output in a file, and print it out in terminal.

    # Creating Here Documents( here text or heredoc)
        - A here document allows you to redirect multiple items into a command. It can also modify a file using script, create a script, keeping data in a script, and so on.
            -"<<" is the here document redirection operator followed by a keyword.
                This keyword can be anything signaling the beginning of the data as well as the the data's end

    # Creating Command Lines
        - xargs utility
            By piping STDOUT from other commands into the xargs utility, you can build command-line commands on the fly.
             example: find tmp -size 0 | xargs /usr/bin/ls
                - xargs requires the program's location
        
        - Shell expansion "$()"
            The first method puts a command to execute within parentheses and precedes it with a dollar sign($).
        
        - The next methods put commands within backticks (`).
        
        - Another method is brace expansion"{}"

# EDITING TEXT FILES

    # Appreciating Text Editors
    
        - nano FILE
            To open a text editor either created prior or edit.
                * Title Bar: The title bar is at the text editor window's top.
                * Main body: Where you perform the editing.
                * Status Bar: The status bar displays status information for the certain events.
                * Shortcut List: The Shortcut List is at the window's button, you can see the most common commands and their associated shortcut keys.
        
        - vim FILE
            - It is a powerful text editor for creating programs or shell scripts.
                * Command Mode: This is the mode vim uses when you first enter the buffer area; also called normal mode.
                * Insert Mode: Insert mode is also called edit or entry mode. Enter by pressing the I key.
                * Ex Mode: This mode is sometimes also called colon commands because every command entered here is preceded with a colon.
    
    # Learning About Stream Editors
        A stream editor modifies text that is passed to it through a file or output from a pipeline.
    
            sed editor : sed [OPTIONS] [SCRIPT]... [FILENAME] e.g echo " I am home" | sed 's/home/tom/'
                    It changes data based on commands either entered into the command line or stored in a text file. The process it goes through is as follows:
                    * Reads one text line at a time from the input stream.
                    * Matches that text with the supplied editor commands.
                    * Modifies the text as specified in the commands.
                    * Outputs the modified text to STDOUT.
            
            If you have a lot of sed script commands, you can store them in a file.
            e.g :
                - cat script.sed( view what is in the created sed file)
                - sed -f script.sed cake.txt

            gawk utility : gawk [OPTIONS] [PROGRAM]... [FILENAME]
                gwak is more powerful editing process via its programming language.
                    * Define variables to store data.
                    * Use arithmetic and string operators to work on data.
                    * Use programming structures, such as loops, to add logic to your processing.
                    * Create formatted reports from data.

                    e.g: echo "Hello World" | gawk '{print $0}'
                            Note: this will print the entire Hello World
                    
                    To modify file: gawk '{if ($4=="cake") {$4="donut"; print $0}}' cake.txt



                    B-C
                    E
                    C,D
                    A
                    D
                    B
                    A,(B,C,E)
                    E
                    B,C-AB
                    C-EC
                    B-C
                    D-E
                    A,C
                    E-B
                    A-D
                    A
                    D
                    B-C
                    C-BCE
                    A,C,E-ACDE

