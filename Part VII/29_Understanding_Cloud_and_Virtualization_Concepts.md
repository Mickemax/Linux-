# Considering Cloud Servcies 
    # What Is Cloud Computing?
        - The term cloud computing is related to distributed computing. In distributed computing, resources are shared among two or more servers to accomplish a single task, such as run an application.
        - This environment became the precursor to what we know today as cloud computing, popularized by companies such as Amazon Web Services, Google Cloud Platform, and Microsoft Azure.
        - The three different methods for providing cloud computing services.
            * Public: In Public cloud computing environments, a third party provides all of the computimg resources outside of the organization.
            * Private: In private cloud computing environments, each individual organization builds its own cloud computing resources to provide resources internally.
            * Hybrid: In Hybrid cloud computing environments, computing resources are provided internally within the organizarion but also connected to an external public cloud to help supplement resources when needed.
    
    # What Are the Cloud Services?
        # Infrastructure as a Service
            - In the infrastructure as a service model, the cloud computing vendor provides low-level server resources to host applications for organizations. These low-level resource include all the physical        componenets oyou'd need for a physical server, including CPU time, and memory space, storage space, and network resources.
        
        # Platform as a Service
            - The cloud computing vendor provides the physical server environment as well as the operating system environment to the customer.
        
        # Software as a Service
            - the cloud computing vendor provides a complete application environment, such as a mail server, database server, or web server.
            - The vendor provides the physical server environment, the operating system, and the application software necessary to perform the function.

# Understanding Virtualization
    # Hypervisors
        - With virtualizarion, you can run multiple virtual smaller server environments on a single physical server. Each virtual server operates as a stand-alone server running on the physical server hardware. This is called a virtual machine (VM).
        - Hypervisor called a virtual machine monitor(VMM), acs as the traffic cop for the physical server resources shared between the virtual machines. It provides a virtual environment of CPU time, memory space, and storage space to each virtual machine running on the server.
    
    # Types of Hypervisors
        # Type I Hypervisors
            - Type I hypervisors are commonly called bare-metal hypervisors. The hypervisor system runs directly on the server hardware, with no middleman. The hypervisor software interacts directly with the CPU, memory, and storage on the system, allocating them to each virtual machine as needed.
            - Two popular Type I Hypervisor packages are:
                * KVM: The Kernel-based Virtual Machine utilizes a standard Linux kernel along with a special hypervisor module, depending on the CPU used. Once installed, it can host any type of guest operating systems.
                * XEN: The Projects is an open source standard for hardware virtualization. Not only does it support Intel and AMD CPUs, but there's also a version for ARM CPUs.
                        - The XEN project includes additional software besides the hypervisor software, including an API stack for managing the hypervisor from a guest operating system.
        
        # Type II Hypervisors
            - Type II hypervisors are commonly called hosted hypervisors because they run on top of an existing operating system install. The hypervisor software runs like any other application on the host operating system.
            - The Type II hypervisor software rubs guest virtual machines as separate processes on the host operating system.
            - The guest virtual machines support guest operating systems, which are completely separated from the host operating system.
            - The attraction of using a Type II hypervidor is that you can run it on an already installed operating system. 
            - You don't need to create a new server environment to run virtual machines. With the Type I hypervisors, you must dedicate a server to hosting virtual machines, while with a Type II hypervisor, your server can perform other functions while it hosts virtual machines.
        
        # Hypervisor Templates
            - The virtual machines that you create to run in the hypervisor must be configured to determine the resources they need and how they interact with the hardware. These configuration settings can be saved to template files so that you can easily duplicate a virtual machine environment either on the same hypervisor or on a separate hypervisor server.
            - The downside to OVF templates is that they are cumbersome to distribute. The solution to that is the Open Virtualization Appliance(OVF) format.
    
# Exploring Containers
    - While utilizing virtual machines is a great way to spin way to spin up multiple servers in a server environment, they're still somewhat clunky for working with and distributing applications.
    - There's no need to duplicate an entire operating system environment to distribute an application.
        
        # What Are Containers?
            - Developing applications requires lots of files. The application runtime files are usually co-located in a single directory, but often additional library files are required for interfacing the application to databases, desktop management software, or built-in operating system functions. These files are usually located in various hard-to-find places scattered arounf the Linux virtual directory.
            - Containers are designed to solve this problem. A container gather all of the files necessary to run an application- the runtime files, library files, database files, and any operating system-specific files. The container becomes self-sufficient for the application to run; everything the application needs is stored within the container.
            - If you run multiple applications on a server, you can install multiple containers.
        
        # Container Software
            - Linux has been in the forefront of container development, making it a popular choice for developers. The are several container packages available in Linux, but here are some of the more popular ones:
                * Podman: The Podman package was developed by Red hat as an open source tool for developing, managing, and running containers. While you can use Podman by itself to run and manage containers, it's also used by other higher-level packages to provide basic container services.
                * containerd: The containerd package is another container manager for smaller container implementations. As the "d" in its name suggests, it runs as a background daemon process on Linux or Windows systems.
                * LXC: The LXC package was developed as an open source standard for creating containers. Each container in LXC is a little more involved that just a standard lightweight application container but not quite as heavy as a full virtual machine, placing it somewhere in the middle.
                * Docker: The Docker package was developed by Docker Incorporated and released as an open source project. Docker is extremely lightweight allowing several containers to run on the same host Linux system that manages the Docker images installed.
        
        # Container Templates
            - Just like virtual machines, containers allow you to create templates to easily duplicate container environments. The different type of Linux containers utilize different methods for distributing templates.
            - The LXC package uses a separate utility called LXD to manage containers. In recent versions, LXD has become so popular that it is now packaged itself as container software, although it still uses the LXC system images of the container.
            - Docker uses Docker container images files to store container configurations. The containe image file is a read-only container image that can store and distribute application containers.
            - The Docker container software package provides an easy platform to run OS containers in your Linux environment. You can only run Linux containers on a Linux Docker host; however, the Docker Desktop package allows you to run Linux or Windows containers on a Windows host.
            - You use the docker command-line tool to easily interact with the Docker system, starting, stopping, and interacting with containers.
            - You can either build a new container image from a Docker configuration file or download a preconfigured container image directly from a container repository, where other admins have posted their containers.
            