## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Red Team Cloud Diagram](Images/red_team_cloud_network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, setup.yml can be modified or run with tags to install certain pieces of the infrastructure to your liking.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_
- _TODO: What does Metricbeat record?_

The configuration details of each machine may be found below.

| Name         | Function                                   | Private IP Address | Operating System         |
|--------------|--------------------------------------------|--------------------|--------------------------|
| Jump-Box     | Ansible provisioner and admin access point | 10.0.0.4           | Linux (Ubuntu 18.04 LTS) |
| Web-1        | DVWA server                                | 10.0.0.5           | Linux (Ubuntu 18.04 LTS) |
| Web-2        | DVWA server                                | 10.0.0.6           | Linux (Ubuntu 18.04 LTS) |
| web-backup   | DVWA server                                | 10.0.0.8           | Linux (Ubuntu 18.04 LTS) |
| DVWA-Backup1 | DVWA server                                | 10.0.0.9           | Linux (Ubuntu 18.04 LTS) |
| DVWA-Backup2 | DVWA server                                | 10.0.0.10          | Linux (Ubuntu 18.04 LTS) |
| ELK-Server   | Hosts ELK docker container and heartbeat   | 10.1.0.4           | Linux (Ubuntu 18.04 LTS) |

### Access Policies

The machines on the internal rednet network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the public workstation IP detailed in RedTeam-SG.

Machines within the rednet network can only be accessed by ssh.

A summary of the access policies in place can be found in the table below.

| Name              | Publicly Accessible | Allowed IP Addresses            |
|-------------------|---------------------|---------------------------------|
| Jump-Box          | Yes                 | workstation public IP port 22   |
| Web VMs           | No                  | 10.0.0.4 port 22                |
| Red_Load_Balancer | Yes                 | workstation public IP port 80   |
| ELK-Server        | Yes                 | workstation public IP port 5601 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. This allows the use of infrastructure as code. Allowing the user to scale their network as large as they want. This also grants the user the ability to modify only a few files and change the configuration of every machine on the network.


The playbook implements the following tasks:
- Set up the ELK-Server with an ELK stack docker container
- Install each web VM with a docker container with an instance of DVWA
- Install Heartbeat on the ELK-VM for up-time metrics
- Install Filebeat, Auditbeat, Packetbeat, and Metricbeat on each web VM
- Configures each machine to send logs to the ELK-Server
- Updates each machine to current packages to ensure system security

The following screenshot displays the result of running `docker ps` on the Elk-Server after successfully configuring the ELK instance.

![Elk container Image](Images/elk_container.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 
- Web-1 10.0.0.5
- Web-2 10.0.0.6
- web-backup 10.0.0.8
- DVWA-Backup1 10.0.0.9
- DVWA-Backup2 10.0.0.10

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat
- Auditbeat
- Packetbeat

**Note**: The ELK-Server has heartbeat installed for up-time metrics as it is advised to install this on a machine not intended to be monitored

These Beats allow us to collect the following information from each machine:
- Filebeat: Collects and forwards system log data to Elk-Server
- Metricbeat: Monitors system metrics like CPU usage, memory, and network acticvity. We have enabled the docker module to watch our DVWA containers as well
- Auditbeat: Interacts directly with and forwards logs from auditd, a system daemon that watches for system changes. It will log file intregity for files found in /etc /usr/bin /bin /usr/sbin and /sbin
- Packetbeat: Analyzes network traffic between systems, sniffing packets providing user with network information
- Heartbeat: Monitors up-time of systems. Will ping each machine on the network on a regular schedule and logs repsonses

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
