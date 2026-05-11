# Building a Python Environment
    - The Python programming lanuage uses an easy-to-understand syntax. Synta refers to the Python commands, their proper order in a Python statement work properly.
    - Python's syntax makes it easy for a beginner to get started programming, but it contains lots of rich and powerful features that make it useful for advanced programmers.

    # Running Pyton Code
        - Python is an interpreted programming language, instead of a compiled language.
        - A compiled programming language has all of its statements turned into binary code before you can run it on the system.
        - An interpreted programming laguage needs another program to read each statement, decode what the statement does, then convert the statement to the binary code that's executed on the CPU.
    
    # The Python Coding Environment
        - The Python interpreter program provides two ways to run Python programs:
            * A development interactive shell provides a prompt that allows you to enter one Python statement at a time to interpret.
            * A production script interpreter program: which is the more practical to use the Python interpreter program.
        - It's the same command-line command, but you include your Python program file on the command line command, but you include your Python program file on the command line.
    
# Python Basics
    # Producing Output
        - You've already seen Python outputs text using the print() function. Previous versions of Python used the print statement, which required a lot of extra effort on the programmer's part to produce output, but version 3.0 changed that with the introduction of the print() function.
        - The basic format of the print() function is simple:
            print(argument)
    
    # Using Variables
        - Storing and manipulating data in a program is done using variables. 
        - A variable is a name that references a memory location where the program stores a value for later use in the script.
        - Variables are defined by a unique variable name in the program. Python has a few rules to follow when creating variable names:
            * You cannot use a Python keyword as a variable name.
            * You can only use uppercase and lowercase letters, numbers, and the underscore character in variable names.
            * The first character of the variable name canot be a number.
            * No spaces are allowed in a variable name.
        - You can store different types of data in variables.
            * Numeric: The numeric data type includes data that contains a numeric value.
            * Boolean: Contains only a True or False value.
            * Sets: An unordered collection of data values.
            * Sequence: The sequence data type includes data that is an ordered collection. This data type includes: str, list, tuple.
            * Dictionary: An unordered collection of data that utilizes a key/value pair.
    
    # Performing Math
        - Python supports all the basic math operators that you would need for normal calculations:

# Advanced Python Features
    # Logic Statements
        - Many programs require some sort of logic flow control between statements. Logic statements allow us to test for a specifc condition, and then branch to different sections of code based on whether the condition evaluates to a True or False logical value.
            if (condition): statement
    
    # Looping Statements
        - The most basic loop statement in Python is the for loop. By default, the for loop iterates through a group of values defined in a data list data type:
            for i in [1,2,3,4,5]:
                square = i*1
                print(square)
        - The while loop allows you to specify a condition that Python tests after each iteration of the loop:
            while condition:
                statemetns
    
    # Creating Functions
        - The format to define a function in Python is 
            def name ( arg1, arg2, ...):
                statements
                return value
        - Just as you would expect in Python, functions rely on indentation in your code to determine which statements are included in the function.
    
# Python Modules
    # Using Modules
        - Since modules are external to your Python code, you need to tell Python to load a specific module to use before you can use the functions contained in the module.
        - You do that with the import statement:
            import module
    
    # Finding New Modules
        - The pip program is the Python module manager. It allowd you to query to the official Python module repository, located at http://pypi.org , then download, install, and remove modules.
        - To query the modules currently installed on your system, use the list command-line option:
        - To seatch for available modules, go to the http://pypi.org website and use the Search feature. Once you find a module you're interested in, use the install option of pip to download and install it.

# The Virtual Python Environment
    - A virtual Python environment  allows you to install module packages into your own Python space, without requiring root access, and without overwriting any other modules that other Python developers on your system have already installed.
        python3 -m venv name
    - To exit the development environment, just use the deactivate command from the Linux command line.
        