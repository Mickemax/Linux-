# Looking at Processes
    - At any given time there are lots of active programss running  on the Linux system. Linux calls each running program a process.
    - A process can run in the background. The Linux system assigns each process a process id (PID) and manages how the process user memory and CPU time based on that PID.
    - You can watch just which process are currently running  on your Linux system by using the ps command.
    - By defaultm the ps command only shows the processes that are running in the current user shell.
    - The current ps program used in Linux supports three different styles of command-line parameters:
        * Unix-style parameters, which are preceded by a dash.
        * BSD-style parameters, which are not preceded by a dash.
        * GNU long parameters, which are preceded by a double dash.
    - One other process feature to pay attention to is the process state. The process state indicates what the program is doing at the moment you checked.
    - There are several process states:
        * Running(R); The program is currently using the CPU to process code.
        * Interruptible Sleep(S): The program is waiting for an external resource ( such as the network or disk), but can be interrupted by the OS.
        * Uniterruptible Sleep(D): The program is waiting for an external resource, but cannot be interrupted by the OS.
        * Stopped(T): The program has terminated.
        * Zombie(Z): The program terminates, but is waiting for the parent program to clear it out of the process table.
                    - This is often confuse with the orphan process( when the parent process has died, but the child process is still active.)

# Monitoring Processes in Real Time
    - The ps command is a great way to get a snapshot of the processes running on the system, but sometimes you need to see more information to get an idea of just what's going on in your Linux system.
    - The top command can solve this problem, it displays process information similar to the ps command, but it does it in real-time mode.
    - The first section of the top output shows general system information. The first line shows the current time, how long the system has been up, the number of users logged in, and the load average on the system.
    - The second line shows general process information(called tasks in top).
    - The next line shows general CPU information. The top display breaks down the CPU utilization into several categories depending on the owner of the process and the state of the processes.
    - Following that, there are two lines that detail the status of the system memory. The first line shows the status of the physical memory in the system, how much total memory there is, how much is currently being used, and how much  is free.
        * The second memory line shows the status of the swap memory area in the system, with the same information.
        * Finally, the next section shows a detailed list of the currently running processes, with some information columns that should look familiar from the ps command output.
    - By default, when you start top it sorts the processes based on thr %CPU value.
    - Use the F or 0 command to toggle which field the sort order is based on.

# Managing Processes

    # Setting Priorities
        - By default, all processes running on the Linux system are created equal: that is, they all have the same priority to obtain CPU time and memory resources.
        - The nice and renice commands allow you to set and change the priority level assigned to and application process.
        - The nice command allows you to start an application with a nondefault priority setting.
            nice -n value command
            * The value parameter is a numeric value from -20 to 19. The lower the number, the higher priority the process receives. the default is 0.
            * The command parameter indicates the program to start at the specified priority:
        - To change the priority of a process that's already running, use the renice command:        
            renice priority [-p pids] [-u users] [-g groups]
        - The renice command allows you to change the priority of multiple running processes based on a list of PID values, all of the processes started by one or more users, or all of the processes started by one or more groups.
    
    # Stopping Processes
        - Sometimes a process hung up, and other times, it runs away with the CPU and refuses to give it up. In both cases, Linux follows the Unix method of interprocess communication.
        - A process signal is a predefined message that processes recognize and may choose to ignore or act on. Table 21.4 shows you different Processs signals.
        - There are two commands available in Linux that allow you to send process signals to running processes.
            # The kill Command
                - The kill command allows you to send signals to processes based on their process ID(PID).
                - By default, it sends a SIGTERM signal to all the PIDs listed on the command line. Unfortunately, you can only use the process PID instead of its command name, making the kill command difficult to use sometimes.
                - The SIGTERM signal only asks the process to kindly stop running. Unfortunately, if you have a runaway process, most likely it will ignore the request.
                - The generally accepted procedure is to first try the TERM signal. If the process ignore that, try the SIGINT or SIGHUP signal.
            
            # The pkill Command
                - The pkill command is a powerful way to stop processes by using their names rather than the PID numbers. The pkill command allows you to use wildcard characters as well, making it a very useful tool when you've got a system that's gone awry.
                        