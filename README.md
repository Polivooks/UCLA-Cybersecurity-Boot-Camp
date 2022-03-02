# UCLA-Cybersecurity-Boot-Camp
This repository "will serve as the location where [I] can store any scripts, diagrams or other documentation that [I] have worked on throughout" my UNIVERSITY OF CALIFORNIA, LOS ANGELES THE CYBERSECURITY BOOT CAMP AT UCLA EXTENSION - LA CAMPUS course.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

*[ELK Stack Project Network Diagram](https://github.com/Polivooks/UCLA-Cybersecurity-Boot-Camp/blob/0902f2c39d9e5b92eba12b8cf8c1804dcb27cb55/Diagrams/ELK_Stack_Project_Network_Diagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

*[ELK Installation File](https://github.com/Polivooks/UCLA-Cybersecurity-Boot-Camp/blob/0902f2c39d9e5b92eba12b8cf8c1804dcb27cb55/Ansible/:etc:ansible:install-elk.yml.rtf)
*[Filebeat Installation File](https://github.com/Polivooks/UCLA-Cybersecurity-Boot-Camp/blob/0902f2c39d9e5b92eba12b8cf8c1804dcb27cb55/Ansible/:etc:ansible:roles:filebeat-playbook.yml.rtf)
*[Metricbeat Installation File](https://github.com/Polivooks/UCLA-Cybersecurity-Boot-Camp/blob/0902f2c39d9e5b92eba12b8cf8c1804dcb27cb55/Ansible/:etc:ansible:roles:metricbeat-playbook.yml.rtf)

This document contains the following details:
1. Description of the Topology
2. Access Policies
3. ELK Configuration

   Beats in Use

   Machines Being Monitored
4. How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA: the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load balancers help to mitigate DoS (Denial-of-service) attacks by receiving incoming traffic to a website and evenly distributing it among multiple servers, all of which are running the same website. A jump box also increases security by providing a safe starting point to which admins may connect *first*, before connecting to potentially riskier servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system metrics.
*Filebeat watches for specified log files or directories.
*Metricbeat records metrics and statistics from a server's OS as well as from services running on the server.

The configuration details of each machine may be found below:

| Name               | Function         | Internal IP Address | Public IP Address                           | Operating System     |
|--------------------|------------------|---------------------|---------------------------------------------|----------------------|
| JumpBoxProvisioner | Jump Box/Gateway | 10.0.0.4            | 20.127.84.187                               | Linux (ubuntu 18.04) |
| Web1               | Server           | 10.0.0.5            | 20.119.35.149 (Load Balancer's Frontend IP) | Linux (ubuntu 18.04) |
| Web2               | Server           | 10.0.0.6            | 20.119.35.149 (Load Balancer's Frontend IP) | Linux (ubuntu 18.04) |
| Web3               | Server           | 10.0.0.7            | 20.119.35.149 (Load Balancer's Frontend IP) | Linux (ubuntu 18.04) |
| ELK                | ELK Server       | 10.1.0.4            | 40.78.69.199                                | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine (JumpBoxProvisioner) can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

*My Personal, Home IP 

Machines within the network can only be accessed by JumpBoxProvisioner.

I allowed 2 machines to access my ELK VM:

1. My MacBook, which accessed my ELK VM from my personal, home IP address, via port 5601; and
2. JumpBoxProvisioner, which accessed my ELK VM from its internal IP address of 10.0.0.4, via port 22 (SSH).

A summary of the access policies in place can be found in the table below:

| Name               | Publicly Accessible? | Allowed IP Addresses                                                                 |
|--------------------|----------------------|--------------------------------------------------------------------------------------|
| JumpBoxProvisioner | Yes                  | My Personal, Home IP (via Port 80)                                                   |
| Web1               | No                   | 10.0.0.4 (JumpBoxProvisioner's IP, via SSH)                                          |
| Web2               | No                   | 10.0.0.4 (JumpBoxProvisioner's IP, via SSH)                                          |
| Web3               | No                   | 10.0.0.4 (JumpBoxProvisioner's IP, via SSH)                                          |
| ELK                | Yes                  | My Personal, Home IP (via Port 5601) and 10.0.0.4 (JumpBoxProvisioner's IP, via SSH) |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous mainly because automation takes complex tasks and simplifies them, freeing-up one's time and energy to be focused where it may be more greatly needed.

The playbook implements the following tasks:
*Configuring the ELK virtual machine with a docker container.
*Installing the Python 3 version of the Docker package.
*Installing the Docker Python module.
*Increasing virtual memory to a maximum value of 262144.
*Downloading and launching a Docker ELK container.
*Enabling Docker service on boot.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[sebp/elk:761](https://github.com/Polivooks/UCLA-Cybersecurity-Boot-Camp/blob/0902f2c39d9e5b92eba12b8cf8c1804dcb27cb55/README_ELK.md/Images/sebp:elk_761.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
*Web1 (IP Address: 10.0.0.5)
*Web2 (IP Address: 10.0.0.6)
*Web3 (IP Address: 10.0.0.7)

We have installed the following Beats on these machines:
1. Filebeat
2. Metricbeat

These Beats allow us to collect the following information from each machine:
*Filebeat collects log events; 'logfile' audit logs are 1 example of what you would expect to see with Filebeat.
*Metricbeat collects OS and service metrics and statistics; 'status' metrics from Apache HTTPD servers are 1 example of what you would expect to see with Metricbeat.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
1. Copy the configuration files from the Ansible container to the Web VMs.
2. Update the hosts file to include the internal IP addresses of each Web VM (webservers) and the ELK VM (elk).
3. Run the playbook, and navigate to http://[your.VM.IP]:5601/app/kibana to check that the installation worked as expected.

**Which file is the playbook? Where do you copy it?**

   The Filebeat configuration file is the playbook. You copy it from /etc/ansible/filebeat-config.yml to /etc/filebeat/filebeat.yml.

**Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?**

   You update the hosts file to make Ansible run the playbook on a specific machine, and you specify which machine to install the ELK server on by on versus which to install Filebeat on by separating the Web VMs into a "webservers" group and the ELK VM into a *separate* "elk" group, both within the hosts file.

**To which URL do you navigate in order to check that the ELK server is running?**

   You navigate to http://[your.VM.IP]:5601/app/kibana in order to check that the ELK server is running.
