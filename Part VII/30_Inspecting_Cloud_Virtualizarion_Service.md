# Focusing on VM Tools
    # Looking at libvirt
        - A popular virtualization management software collection is libvirt library. This assortment includes the following elements:
            * An application programminf interface (API) library that is incorporated into several open source VMMs(hypervisors), such as KVM.
            * A daemon, libvirtd, that operates on the VM host system and executes any needed VM guest system management tasks, such as starting and stopping the VM.
            * Command-line utilities, such as virt-install and virsh, that operate on the VM host system and are used to control and manage VM guest systems.
        - While typically most command-line utilities that start with vir or virt employ the libvirt library, you can double-check this via the ldd command.
    
    # Viewing virsh
        - One handy tool that uses the libvirt library is the virsh shell. It is a basic shell you can employ to manage your system's virtual machines.
        - If you have a VMM product installed, you can employ the virsh shell to createm removem startm stop, and manage your virtual machines.
    
    # Managing with Virtual Manager
        - Not to be confused with a hypervisor,The Virtual Machine Manager is a lightweight desktop application for creating and managing virtual machines.
        - It is a Python program available on many distributions that employ a GUI and is obtainable from the virt-manager package.
        - The Virtual Machine Manager can be initiated from a terminal emulator within the graphical environment via the virt-manager command.
        - You do not need to use super user privileges to run the Virtual Machine Manager, and if the virt-manager command is not issued from an account with those privileges, it will provide a pop-up window asking for the root account password or something similar, depending on the distribution.

# Understanding Bootstrapping
    - A bootstrap is a small fabric or leather loop on the back of a shoe. Nowadays you yse them to help pull shoe onto your foot by hooking your finger in the loop and tugging. A phrase developed from that little tool, "Pick yourself up by your bootstraps," which means to recover from a setback without any outside help.
    - Bootstrapping a system refers to installing a new system using a configuration file or image of an earlier system install.

        # Booting with Shell Scripts
            - Whether you are creating guest virtual machines in the cloud or on your own local host machine, there are various ways to get them booted. 
            - Starting a few VMs via a GUI is not too terribly difficult, but if your company employs hundred of virtual machines, you need to consider automating the process.
            - Using shell scripts fr booting virtual machines is typically a build-your-own approach, though there are many examples on the Internet,
        
        # Kick-Starting with Anaconda
            - You can quickly and rather easily bootstrap a new system using the kickstart installation method. This RHEL-based technique for setting up and conducting a system installation consists of the following:
                - Creating a kickstart file to configure the system
                - Store the kickstart file on the network or on a detachable device, such as a USB flash drive.
                - Place the installation source where it is accessible to the kickstart process.
                - Create a boot medium that will initiate the kickstart process.
                - Kick off the kickstart installation.
        
        # Initializing with Cloud-init
            - Cloud-init is a Canonical product. It provides a way to bootstrap virtualized machines. Canonical on its cloud-init website, http://cloud-init.io, describes it best: " Cloud images are operating system templates and every instance starts out as an identical clone of every other instance. It is the user data that gives every cloud instance its personality and cloud-init is the tool that applies user data to your instances automatically."
            - The /etc/cloud/cloud.cfg file is the primary cloud-init configuration file. The command-line utility name is, as you might suspect, the cloud-init command.

# Exploring Storage Issues
    - When setting up your virtual system, it is critical to understand the various virtual disk configuration options. The choices you make will directly affect the virtual machine's performance. 
    - Several virtualization services and products have a few terms you need to understand before making these configurations:
        * Provisioning: When a virtual machine is created, you choose the amount of disk storage. However, it is a little more complicated than simply selecting the size. Virtual disks are provisioned either thinly or thickly.
            - Thick provisioning is a static setting where the virtual disk size is selected and the physical file(s) created on the physical disk is preallocated.
            - Thin provisioning is grown dynamically, which causes the hypervisor to comsume only the amount of disk space actually used for the virtual drive.
        * Persistent Volumes: The term persistent volume is used by many virtualization products, sucj as OpenStack and Kubernetes. In essence, a virtualized persistent volume is similar to a physical fisk how it operates.
        * Blobs: Blob storage is a Microsoft Azure cloud platform term. Blobs storage is large unstructured data, which is offered over the Internet and can be manipulated with .NET code.
            - Blob data items are grouped together into a container for a particular user account and can be one of three different types:
                * Block blobs are blocks of text and binary data. The blobs are not managed as a group but instead are handled independently of one another.
                * Append blobs are also blocks of text and binary data. However, their storage is enhanced to allow for efficient appending operations. Thus, this blob type is often used for logging data.
                * Page blobs are somply random access filesm which can be ip to 8TB in size.

# Considering Network Configurations
    # Virtualizing the Network
        - Network virtualixation has been evolving over the last few years. While it used to simply mean the virtualization of switches and routes running at OSI levels 2 and 3, it can now incorporate firewalls, server load balancing, and more at higher OSI levels.
        - Twp basic network virtualizarion concepts are virtualized local area networks ( VLANs) and overlay networks:
            * VLAN: To understand a VLAN, it is best to start with a local area network(LAN) description. A VLAN consist of systems and various devices on a LAN. 
                - However, this group of systems and various devices can be physically located across various LAN subnets.
            * Overlay Network: An overlay network is a network virtualization method that uses encapsulation and communication channel bandwith tunneling. A network's communication medium is virtually split into different channels.
                - Each channel is addigned to a particuar service or device. Packets traveling over the channels are first encapsulated inside another packet for the trip.
    
    # Configuring Virtualized NICs
        - Virtual NICs (adapters) are sometimes directly connected to the host system's physical NIC. Other times they are connected to a virtualized switch, depending on the configuration and the employed hypervisor.
        - When configured a virtual machine's NICm you have lots of choices. It is critical to understand your options in order to make the correct selections.
            * Host-Only adapter connects to a virtual network contained within the virtual machine's host system. Theree is no connection to the external physical network to which the host system is attached
            * Bridged NIC makes the virtual machine like a node on the LAN or VLAN to which the host system is attached. The VM gets its own IP address and can be seen on the network.
            * NAT: A network address translation adapter configuration operates in a way that's similar to how NAT operates in the physical world. The NAT table is maintained by the hypervisor instead of a network device. Also, the IP address of the host system is employed as the single IP address that is sent out onto the external network.
            * Dual-Homed: In the physical world, a dual-homed system is a computer that has one or more active network adapters. Often a physical host is configured with multiple NICs. This configuration provides redundancy.
                - In the virtual world, many virtual machine are dual-homed, depending on the virtual networking environment configuration and goals.
                - The physical and virtual machine network adapter configuration has performance and security implications. Understanding your internal virtual and external physical networks and goals is an important part of making these choices.

            