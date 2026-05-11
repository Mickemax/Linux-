# Focusing on the GUI
    - GUI is a series of components that work together to provide the graphical setting for the user interface (UI). One of this is desktop environment which provides a predetermined look and feel to the GUI.
        - Desktop Settings: programs that allow you to make configuration changes to the desktop.
        - Display Manager: desktop environment's login screen is where you choose a username and enter a password to gain system access.
        - File Manager: , - Icons:, - Favorites Bar: , - Launch:, Menus, Panels, System Tray, Widgets, Window Manager.
    
    # Getting to Know GNOME
        - The GNOME desktop environment is very popular and found by default on linux distributions such as CentOS and Ubuntu.
    
    # Probing KDE Plasma 
        - The Kool Desktop Environment, this was no longer just referring to a desktop environment, but instead it specified the project's organization and the strong community that supported it.
    
    - Many desktop environments have multiple UIs called workspaces available for each user. Workspaces are individual desktops.

    # Setting Up Accessibility
        - In a GUI environment, accessibility deals with a user's ability to use the desktop environment.
        - Each desktop environment will provide slightly different methods for configuring accessibility, but most are through the contol panel.
            - For users with serious visual impairments or just poor eyesight, several accessibilty settings may help.
                * If blind user has access to a braille display, you can install the brltty package, which is available in most Linux distribution's repositories.
            - AccessX was a program that provided many of the options for users with hand and/or finger impairments.
    
    # Serving Up the GUI
        - A window manager is a program that communicates with the display server ( sometimes called a windows manager) on behalf of the UI. 
            - Each particular desktop environment has its own default window manager; Mutter, Kwin, Muffin, Marco, and Metacity.
        - The display server, a program(s) that uses a communication protocol to transmit the desires of the UI to the operating system, and vice versa.
        - The communication protocol is called the display server protocol and can operate over a network. A compositor program arranges various display elements within a window to create a screen image to be passed back to the client.

    # Figuring Out Wayland
        - Replacement for X11 display server, it is designed to be simpler, more secure, and easier to develop and maintain. 
        - It defines the communication protocol between a display server and its various clients.
        - Weston is Wayland compositor which core focus is correctness and reliability.
                    # Troubleshooting Techniques for with GUI issues using wayland;
                        - Try the GUI without wayland:  
                                * If you do not have multiple flavors of the desktop environment and you are using the GNOME Shell user interface, turn off Wayland. /etc/gdm3/custom.conf file, removing the # from the #WaylandEnable=false.
                                * If you have log out of your GUI session and pick the desktop environment without Wayland.
                        - Check your system's graphics card:
                                * Check if graphic card vendor supports Wayland.
                        - Using a different compositor:
                                * If you are using a desktop environment built-in compositor or one of the other compositors, try installing and using the Weston compositor package instead.
    
    # Examing X11
        - The dominant server implementing X Window System ( X) was XFree86, when a licensing change occured which caused many Linux distribution to switch to the X.Org foundation's implementation of X.
        - The X11 configuration file is /etc/X11/xorg.conf, though it sometimes is stored in the /etc/ directory. Typically this file is no longer used.
            - Instead, X11 creates a session configuration on the fly using runtime autodetection of the hardware involved with each GUI's session.
        - In some cases, autodetect might not work properly and you need to make X11 configuration changes.
        - Desktop environment also provide dialog boxes in their UI, which allow you to configure your GUI X sessions. view "man 5"
            - If you need to troubleshoot X problems, two utilities can help: xdpyinfo(provides information about the X server, including the different screen type available, the default communication parameter values, protocol extension information) and xwininfo( is focused on providing window information. If no options are given, an interactive utilitu asks you to click the window for wich you desire statistics).

    # Using Remote Desktops
        - Uses a client/server model. the server runs on the remote Linux system, while the client runs on the local system.

            # Viewing VNC
                - Virtual Network Computing(VNC) is multiplatform and employs the Remote Frame Buffer(RFB) protocol. This allows a user on the client side to send GUI commands, such as mouse clicks, to the server.
                - The VNC server offers a GUI service at TCP port 5900+n, where n equals the display number, usually port 1.
                - VNC has a lot of Benefits;
                - Also there are potential difficulties or concenns with VNC;
                - Once you have a TigerVNC installed, you control it with the vncserver and vncconfig commands. After making the appropriate server firewall modifications, the client can use the vncviewer command to connect to the server system and get a remote desktop.

            # Grasping Xrdp
                - An alternative to VNC, It supports the Remote Desktop Protocol(RDP) and uses X11rdp or Xvnc to manage the GUI session.
                - Xrdp provides only the server side of an RDP connection.
                - It comes system ready.
                - Note: Read note on installation.

            # Exploring NX
                - The NX protocol, sometimes called NX technology, was created by NoMachine. NX is another remote desktop sharing protocol.
                - Some of its benefit are on the book.

            # Studying SPICE
                - Another interesting remote connection protocol is Simple Protocol for Independent Computing Environments (SPICE).
                - SPICE is platform independent and has some nice additional features as well:
                - SPICES has strong security features.

            # Forwarding
                - Providing data access to only those who are authorized is imperative.
                - One way to provide security is via SSH port forwarding, sometimes called SSH tunneling.
                - SSH port forwarding comes in the following three flavors:
                    * Local:
                        - Local port forwarding sends traffic from the OpenSSH client on your system to the client's OpenSSH server.
                        - The client's OpenSSH server then forwards that traffic on to the destination server via a secured tunnel.
                            * The -L option of the ssh command is used along with some additional arguments.
                            *
                    * Remote
                    * Dynamic             