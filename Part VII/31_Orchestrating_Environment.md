/*Orchestration refers to the organization of a process that is balanced and coordinated and achieves consistency in the results. */

# Understanding Orchestration Concepts
    - One particular IT orchestration process, which is getting a lot of attention these days, is DevOps. This method improves software delivery operations.
        * Continuous integration
        * Continuous testing
        * Continuous delivery( or deployment)
        * Infrastructure as Code
        * Infrastructure automation
        * Monitoring and logging

        # Probing Procedures
            - In DevOps, the idea is to quickly and continually provide new software features, bug fixes, and desired modifications to the customer.
            - The focus is on continual small changes to the app as opposed to large monolithic updates.
                * Continual App Processing: One DevOPs layer involves softwae revision control that quickly integrates app changes into the main software branch (continuous integration).
                * Controlling the App Environment To support this continuous app processing layer, it is critical in DevOps that the development hardware, device drivers, operating system versions, software librariesm and so on.
                    - The requirement provides a software development environment that produces production code freem from bugs and complications due to mismatched environments.
                * Defining the App Environment In DevOPs, the development and production environments(infrastructure) have predefied specifications, such as what hardware to employ, the essential operating system, and any needed software packages as well as critical code libraries.
                - The non-hardware specifications are typically implemented into the environment via automated code( configuration management).
                * Deploying the App Environment The app and its development environment are often moved to a production status( production environment) in a continual manner. The "continual manner" can be hourly daily, weekly or whatever meets the app's business requirements.
                * Monitoring the App Environment When the app is operating in its production environment, it needs to be monitored and logged. Software metrics, infrastructure resource usage, and performance statistics are just a few of the items to monitor and log.
        
        # Analyzinf Attributes
            - Virtualization and more specifically, containers greatly assist in the DevOps process. Containers in DevOps provide the following:
                * Statis Environment: Containers provide a predetermined app environment that does not change through time. The container is created with preset library and operating system versions and security settings. 
                * Version Control: After the software development process and prior to moving a modified app container image into production, the container and its recorded configuration are registered with a version control system.
                * Replace, Not Update: After registration, the app container is ready to move into production. Instead of the production app container image being updated to match the development image, the production container is stopped. The development app container image then replaces the production container and starts as the production environment.
                * High Availability: Replication is the process of creating multiple copies of the production app container image and running them. This allows you to stop old currently unsued production app containers and replace them with the new production app containers, which provides continual uptime for your app users.

# Provisioning the Data Center
    # Coding the infrastructure
        - Much like a physical data center, a container infrastructure needs to be managed and controlled. In orchestration, the container's configuration is treated in a manner similar to how software revisions are treated.
            * Determine the Infrastructire Along with the app requirements, the environment on which the app is executed must be preplanned. This activity is mutual one between software development and tech ops.
            * Document the Infrastructure The preset app container infrastructure is typically documented through an orchestration tool. The configuration management and policy as code settings are loaded into the utility;s infrastructure as code portal, in a process called automated configuration managment. The data is later used to deploy and replicate the app contaierns through build automation.
            * Provide Revision Control: The infrastructure as Code infrastructure is not just documented. It is also inserted into an orchestration tool registry, providing version control. Every time a change occurs in the container image infrastructure, its modifications are tracked.
            * Troubleshoot the Infrastructure: If an app container is deployed into production and problems occur, tech ops, software developers, or both handle the troubleshooting proces.
    
    # Automating the Infrastructure
        - With orchestration tools and automated configuration management, you cna easily replicate the production app container and don't even have to be involved in the process. You simply let your orchestration tool know that you need X number of production app container images running at any one time.
        - A few of the more popular automation utilities in use today are:
            * Ansible: which uses OpenSSH and Python to communicate using JSON-based protocols to remote servers.
            * Chef: A Ruby-based package that uses Ruby-based "recipes" for defining server configurations. Can run in either a client-server mode or a stand-alone mode.
            * Puppet: uses its own language to define system configurations for remote servers, thus requiring little to no programming knowledge to configure.
            * SaltStack: Owned by VMWare, it is a Python-based configuration management tool that stores server configuration data in YAML data structures.
            * OpenTofu: Managed by the Linux Foundation, it is a fork of the commercial Terraform automation utility by HashiCorp. It uses the standard JSON data format to define server configuration data.

    # Comparing Agent and Agentless
        - Orchestration monitoring, logging, and reporting tools let you track app containers' health. Concerns over how these tools may adversely affect an app container's health gave rise to the agent versus agentless dispute.
        - Agent monitoring are orchestration utilities that require software( an agent) to be installed in the app container being monitored. THese agents collect the data and transmit it to another location, such as a monitor server.
        - Agentless monitoring tools are also orchestration utilities. In this case, an agent is not installed in the app container being monitored. Instead, the tool uses preexisting and/or embedded software in the container or the container's external environment to conduct its monitoring activity.
    
    # Investigating the Inventory
        - Orchestration monitoring utilities can automatically deal with an app container's untimely demise. When an app container shuts down, this triggers an event, and the desired state is no longer met. A containers should be deployed and running.
        - Many orchestration utilities employ self-healing. With self-healing, if the desire state is not currently being achieved, the orchestration tool can automatically deploy additional production app containers.

# Looking at Container Orchestration Engines
    - Orchestration of containers, whether the containers are on your local server or in the cloud, requires various orhestration engine.
    - No one system can do it all. The best combination is a set of general and specialized orchestration tools.

        # Embracing Kubernetes
            - Originally designed and used by Google, Kubernetes is open-source orchestration syste, that is considered by many to be the de facto standard. It is highly scalable, fault tolerant, and ( relatively) easily to learn.
            - This system contains years of Google's orchestration experience, and because it is open source, additional community-desired features have been added. This is one reason so many companies have adopted its use for container orchestration.
                * Cluster service: Uses A YAML file to deploy and manage app pods.
                * Pod: Contains one or more running containers.
                * Service: A single instance of a running application containter
                * Worker: Pod host system that uses a kubelet (agent) to communicate with cluster services.
                * YAML file: Contains a particular app container's automated configuration management and desired state settings.
            - The YAML configuration file defines setting used in all the pods in the cluster. This includes the number of replicas for each service required, any custom network settings, shared storage volume settings, secrets( which allow you to encrypt passwords used in services), log files, and system variables set in each container.
        
        # Checking into Docker Compose
            - While Docker Container runs and amanges multiple containers similar to Kubernetes,, it can only do so on the same physical server. to manage multiple containers on separate physical servers Docker has another pacakge, described in the next section.
        
        # Inspecting Docker Swarm
            - Docker, the popular app container management utility, created its own orchestration system for managing containers running on separate physical servers called Docker Swarm, similar to Docker Compose, application containers are called services, and each physical server is called a node. 
            - A group of Docker containers is referred to as a cluster, which appears to a user a singlw container.
            - With the Swarm system, you can monitor the cluster's health and return the cluster to the desired state should a container within the cluster fail.
     

