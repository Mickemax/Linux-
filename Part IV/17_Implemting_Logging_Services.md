/* This chapter explores the two most popular logging methods used in Linux distributions, rsyslog and systemd-journald. */

# Understanding the Importance of Logging
    - All Linux distributions implement some method of logging. 
    - Logging directs short messages that indicate what events happen, and when they happen, to users, files, or even remote hosts for storage.

    # The syslog Protocol
        - In the early days of Unix, myriad logging methods were used to track system and application events.
        - Applications used different logging methods, making it difficult for system administrators to troubleshoot issues.
        - The syslog was used, for logging events from a Sendmail mail application. Eventually quickly became a standard for logging both system and application event in Unix and made its way to the Linux world.
        - syslog protocol defines a standard message format that specifies the timestamp, type, severity, and details of an event. That standard can be used by the operating system, applications, and even devices that generate errors.
        - The type of event is defined as a facility value. The facility defines what is generating the event message, such as a system resource or an application.
        - Each event is also marked with a sevrity which defines how important the message is to the health of the system.

# Basic Logging Using rsyslog
    - The rsysog application uses all the features of the original syslog protocol, including the configuration format and logging actions.
    - It was created as an improvement to the original syslogd program used by legacy Linux systems.
        
        # Configuration
            - The rsyslog package uses the rsyslogd program as a replacement for the original syslogd program. 
            - It monitors events and logs them as directed, using the /etc/rsyslog.conf configuration file to define what events to listen for and how to handle them.
            - Many Linux distributions also use an /etc/rsyslog.d directory to store individual configuration files that are included as part of the rsyslog.conf configuration.
            - The configuration file contains rules that define how the program handles syslog events received from the system, kernel, or applications.
                - the format of an rsyslogd rule is as follows:
                    facility.priority action
                - The facility entry uses one of the standard syslog protocol facility keywords.
                - The priority entry uses the severity keyword as defined in the syslog protocol, but with a twist.
                    - When you define a severity, syslogd will log all events with that severity or higher(lower severity code). Thus the entry
                       kern.crit
                    - To log only messages with a specific severity,use an equals sign before the priority keyword:
                        kern.=crit
                - The action entry defines what rsyslogd should do with the received syslog message. There are six action options available to you:
                    - Forward to a regular file
                    - Pipe the message to an application.
                    - Display the message on a terminal or the system console.
                    - Send the message to a remote host.
                    - Send the message to a list of users.
                    - Send the message to all logged-in users.
        
        # Making Log Entries
            - If you create and run scripts on your Linux system you may want to log your own application events.
                logger [-isd] [-f file] [-p priority] [-t tag] [-u socket] [message]
            - On a Rocky system, you can look at the end of the /var/log/messages file to see the log entry.
        
        # Finding Event Messages
            - Depending on the security if the Linux systen, some log files are readable by everyone, but most may not be.
            - It is also common for individual applications to have a separate directory under the /var/log directory for their own application event messages, such as /var/log/apache2 for the Apache web server.

    
# Journaling with systemd-journald
    - The systemd system services package includes the systemd-journald journal utility for logging.
    - The systemd-journald program uses its own method of storing event messages, completely different from how the syslog protocol specifies.

        # Configuration
            - The systemd-journald service reads its configuration from /etc/systemd/journald.conf configuration file.
            - When you examine this file, you'll notice that there aren't any rulws defined, only settings that control how the application works:
                - The Storage setting determines how systemd-journald stores event messages. When the setting is set to auto, it will look for the /var/log/journal directory and store event messages there.
                - If that directory doesn't exist, it stores the event messages in the temporary /run/log/jounal directory, which is deleted when the system shuts down. You must manually create the /var/log/journal directory for the event messages to be stored permanently.
                - The Compress setting determines whether to compress the journal files.
                - There are several file maintenace settings that control how much space the journal is allowed to use as well as how often to split journal files for archive, based on either time or file size.
                - The ForwardToSyslog setting determines if systemd-journald should forward any received messages to a separate syslog program. such as rsyslogd, running on the system. This provides two layers of logging capabilities.
                - There are quite a few settings that allow you to customize exactly how systemd-journald works in your system.

        # Viewing Logs
            - The systemd-journald program doesn't store journal entries in text files. Instead it uses its own binary file format that works like a database.
            - The journalctl program is our interface to the journal files. The basic format for the journalctl command is as follows:
                journalctl [options] [matches]
                - The options control data returned by the matches is displayed.
                - The journalctl command is great for when you are looking for specific event entries in the journal; it allows you to filter out events using the matches and determine how to display them using the options.

# Monitoring Linux Systems
    - Log aggregation is the proccess of combining log entries from multiple servers into a single location. There are two basic methods for log aggregation:
        - In the agent-oriented method, the monitored server runs a program in the background(called the agent) that pushes log error events to a central location as they occur.
        - In the agentless method, the central location server actively polls each monitored server at predetermined intervals to look for error events.
            There aer many different ways of aggregation log data. Here aer two most popular:
                - The Simple Network Management Protocol(SNMP): SNMP can be used in either the agent-oriented or agentless methods. In the agent-oriented method, you must configure the SNMP program on the monitored server to look for specific events, and when they occur, the SNMO program forwards the event to the central server.
                - Webhooks: Webhooks are simple application programming interfaces (APIs) that communicate using common web protocols such as HTTP and JSON.
        - Orgamizations often have service requirements for tracking application availability, making server monitoring a must.
            - Service-level agreement(SLA): A contract between the service provider and customer, outlining the description of the service.
            - Service-level objective(SLO): Defines the metrics to monitor ( such as application uptime or latency), the expected target levels, and the reported methods.
            - Service-level indicator(SLI): The measurable features of the system that determine if the SLO is being met, such as CPU load and network load.

