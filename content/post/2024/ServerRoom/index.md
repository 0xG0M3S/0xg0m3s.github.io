+++
title = 'Building My Homelab: Hardware, Setup, and Future Plans'
date = 2024-08-30T18:43:41-05:00
tags = ['lab']
#draft = true
+++

Embarking on my journey into web security and networking, I've taken a significant step by acquiring three Dell PowerEdge R740xd servers and other hardware on an auction. Now, this hardware forms the backbone of my new homelab, where I plan to explore, experiment, and document my experiences. In this post, I'll walk you through the specs of my setup, the roles I've assigned to each server, and some ideas I have for future projects.

## Hardware Overview

### Servers: Dell PowerEdge R740xd

The cornerstone of my homelab is the trio of Dell PowerEdge R740xd servers. These robust machines offer impressive performance and scalability, making them ideal for a variety of tasks within my setup.

![Dell](https://i.dell.com/is/image/DellContent//content/dam/images/products/servers/poweredge/r740xd/dellemc-per740xd-24x25-bezel-2-lf.psd?fmt=png-alpha&pscan=auto&scl=1&imwidth=250)

#### Node breakdown

#### Node 1 & 2 - Key Specifications:

* Processor: Dual Intel(R) Xeon(R) Gold 6152 (22 cores each)
* Memory: 256GB DDR4 RAM
* Storage:
    - 2.5” bays
* Networking: 
    - DELL BroadCom 5720-t rNDC 4-Port Gigabit
    - BroadCom GbE 2-Port 5720-t Adapter

#### Node 3 - Key Specifications:

* Processor: Dual Intel(R) Xeon(R) Silver 4215 (8 cores each)
* Memory: 128GB DDR4 RAM
* Storage:
    - 3.5” bays
* Networking: 
    - DELL BroadCom 5720-t rNDC 4-Port Gigabit
    - BroadCom GbE 2-Port 5720-t Adapter

### Networking: 24-Port Gigabit Switch
To facilitate seamless communication between the servers and other devices in the network, I’ve integrated a 24-port Gigabit switch. Each server connects to the switch via at least three Ethernet cables, which I plan to aggregate using a Link Aggregation Group (LAG) interface. This setup will enhance bandwidth and provide fault tolerance, ensuring that my homelab remains robust and reliable.

### Storage Array: Dell EMC PowerVault ME4024

Right now, this storage array is shut down because I don't have compatible disks for it. Initially, I planned to use my spare disks to connect to the server in a JBOD or RAID 5 configuration. However, I discovered that the array is locked to specific enterprise models from Dell and other manufacturers, making consumer-grade disks incompatible. I’m considering whether to purchase the appropriate disks to explore this system further or simply sell it. The final decision is still up in the air.

## The Hypervisor: Proxmox

Initially, I considered VMWare ESXi, but due to licensing changes earlier this year, I opted for Proxmox as my hypervisor.
Installing Proxmox on the Dell servers was straightforward, and it offers a user-friendly interface to manage virtual machines (VMs) and containers efficiently.

I choose Promox because it offers:

- Flexibility: Supports both KVM for full virtualization and LXC for lightweight containers.
- Clustering: Easily manage multiple servers as a single cluster.
- Community Support: Extensive documentation and a supportive community make troubleshooting and expanding my setup easier.
- Web-based interface: I can do all management tasks with the integrated graphical user interface (GUI)
- Based on Debian GNU/Linux

## Network Configuration

With multiple Ethernet connections per server, I plan to set up a LAG interface, since all nodes have six 1 Gib ports and I've connected them using 3 port to the switch. By aggregating these connections, I aim to:

- Increase Bandwidth: Combine the throughput of multiple ports to handle higher data loads.
- Enhance Redundancy: Ensure network availability even if one or more links fail.

Configuring LAG on Proxmox should be relatively straightforward, and I’m looking forward to testing its performance in my homelab environment.

## Future Plans

As I continue to build and expand my homelab, I’m excited to explore the following:

- Infrastructure as Code (IaC): Automating the creation and configuration of virtual machines, containers, and entire environments within my homelab. This will streamline my processes and enable me to experiment with complex setups effortlessly.

- Network Simulation: Using GNS3, I aim to simulate various network configurations, study new algorithms, and prepare for certifications like the CCNA.

- Expanding NAS Capabilities: Beyond file storage, I’m considering how Node 3 can serve other roles, such as media storage, backups, or even a private cloud solution.

### Exploring Infrastructure as Code (IaC)

One of my key goals is to implement Infrastructure as Code (IaC) to automate the creation and management of my labs. By using tools like Terraform or Ansible, I plan to:

Automate VM and Container Deployment: Quickly spin up environments tailored to specific projects or experiments.
Ensure Consistency: Maintain uniform configurations across different setups, reducing the potential for errors.
Streamline Management: Simplify updates and changes, making my homelab more efficient and scalable.

### Network Simulation with GNS3

Networking is a critical component of my transition into web security, and I’m eager to explore network simulation tools like GNS3. Here’s how I plan to utilize Node 1:

Network Design and Testing: Simulate complex network topologies to test configurations and troubleshoot issues before deploying them in a live environment.
Studying Network Algorithms: Dive deep into how different protocols and algorithms function, enhancing my understanding for future certifications.
CCNA Preparation: Use simulated environments to practice and prepare for the Cisco Certified Network Associate (CCNA) exam.

## Node Assignments and Future Plans

I’ve designated specific roles for each of my three servers to optimize their use:

- Node 1: Dedicated to running GNS3 and other network simulators. This setup will be the playground for experimenting with network configurations and simulations.
- Node 2: Intended to host various services and applications. This could include additional VMs, containers, or specialized tools for cybersecurity tasks.
- Node 3: Configured as a Network Attached Storage (NAS) using TrueNAS. With its 3.5” bays, Node 3 will handle file storage, backups, and serve as a reliable repository for my projects.

## Showcasing Possibilities and Ideas

With this robust hardware and thoughtful configuration, the possibilities are vast:

- Comprehensive Cybersecurity Labs: Simulate real-world security scenarios to practice and hone my skills.
- Automated Deployments: Utilize IaC to streamline the setup of complex environments, making it easier to replicate and scale labs.
- Advanced Networking Projects: Explore new network protocols, algorithms, and configurations, laying the groundwork for advanced certifications like CCNA.
- Data Management and Backup Solutions: Leverage Node 3 for efficient data storage, backup solutions, and file sharing across the network.

# Conclusion

Setting up a homelab is an exciting venture that combines hardware prowess with creative and technical challenges. With my new Dell R740xd2 servers, Proxmox as the hypervisor, and a strategic network setup, I’m well on my way to building a versatile and powerful environment for learning and experimentation. Stay tuned for more detailed posts on each aspect of the setup, including step-by-step guides, troubleshooting tips, and reflections on the journey.

---

# Brainstorming Questions

As I continue to develop my homelab, I’d love to hear your thoughts and ideas:

- What additional services or applications should I consider hosting on Node 2 to maximize its potential?
- Are there any specific Infrastructure as Code tools or frameworks you recommend for automating homelab deployments?
- How can I best utilize Node 3’s storage capabilities for both backups and active projects without compromising performance?
- What are some advanced networking projects or simulations that could help me prepare for the CCNA certification?
- How can I integrate security tools and practices into my homelab to enhance my learning in web security?

Feel free to share your insights and suggestions in the comments below. Let’s build a community of learners and innovators together!

- What other tools or platforms should I consider for network simulation and testing?
- How can I further optimize my NAS setup for performance and redundancy?
- What are some advanced use cases for Infrastructure as Code that I should explore?
- Are there any emerging technologies in network security that I should integrate into my homelab?
- How can I leverage my homelab to prepare for and pass the CCNA certification?

Thank you for joining me on this journey! I’m looking forward to sharing more insights and discoveries as I continue to explore the potential of my homelab.

Topics

- hardware
    - about Dell RX740d
    - Switch
- virtualization
    - Promox
    - vmware esxi