# Focusing on the GUI
	# Local
		- Local port forwarding sends traffic from the OpenSSH client on your system to the client's OpenSSH client on your system to the client's OpenSSH server.
			- To enact this on the command line, the -L option of the ssh command is used along with some additional arguments.
				- Keep in mind that this command only establishes the tunnel-it does not provide a remote desktop connection.
			- The -N option let OpenSSH know that no remote terminal process is desired, whereas the -f option indicates the after the user is authenticated to the server, the ssh command should move into the background.
			- TigetrVNC employs the -via localhost option on the vncviewer command. The -via localhost option used in conjunction with the vncviewer command forces the connection to use local SSH port forwarding.

	# Remote
		- The remote SSH port forwarding method starts at the destination host ( server), as opposed to the remote client.

	# Tunneling Your X11 Connection
		- X11 forwarding allows you to interact with various X11-based graphical utilities on a remote system through an encrypted network connection.
		- Go to the OpenSSH configuration(/etc/ssh/sshd_config) file to see if the X11 forwarding is permitted.
		- the ip addr show command is employed for this purpose.
