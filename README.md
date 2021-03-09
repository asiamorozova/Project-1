## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

/Users/anastasiamorozova/Project-1/Diagrams/Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

/Users/anastasiamorozova/Project-1/Ansible/filebeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

 - A jumpbox or bastion server functions as a gateway to gain entry into a remote network. Many times the primary mode of access is ssh and requires a key, otherwise access is forbidden.
 
 - A loadbalancer is meant to serve as a specific point of access for a service that is utilized by multiple machines, allowing high availability models to function propertly.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
- Filebeat is meant to primarely watch for system logs and forward any changes to the Elasticsearch Host.
- Metricbeat is used for gathering metrics and system resources usage to be displayed in Elasticsearch Host. 

The configuration details of each machine may be found below.


|  Name      |  Function             |  IP Address  |  Operating System  |
|------------|-----------------------|--------------|--------------------|
|  Jump Box  |  Gateway              |  10.0.0.4    |  Linux             |
|  Web-1     |  Web Server           |  10.0.0.5    |  Linux             |
|  Web-2     |  Web Server           |  10.0.0.6    |  Linux             |
|  Web-3     |  Web Server           |  10.0.0.7    |  Linux             |
|  ELK       |  ElasticSearch Stack  |  10.1.0.4    |  Linux             |    |          |            |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox/JumpboxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- my public IP

Machines within the network can only be accessed by jumpbox/JumpboxPovisioner.
- Public IP: 13.68.190.137 & Private IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

|  Name      |  Publicly Accessible    |  Allowed IP Addresses  |
|------------|-------------------------|------------------------|
|  Jump Box  |  Yes (SSH, Port 22)     |  24.22.95.219          |
|  Web-1     |  No                     |  40.121.108.109        |
|  Web-2     |  No                     |  10.0.0.6              |
|  Web-3     |  No                     |  10.0.0.7              |
|  ELK       |  Yes (Kibana via 5601)  |  10.1.0.4              |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous, because by automating configuration with Ansible, allowed full automation and reduced configuration errors.

The playbook implements the following tasks:
- Install Docker: Installs the core docker code to the remote server
- Install Python3_pip: Pip is an installation module that allows for additional docker modules to be installed easier
- Docker Module: Tells the previous PIP module to install the necessary docker component modules
- Increase Memory/Use More Memory: A common issue with the ELK Docker image is to little memory.   This help fix the issue to allow the server to launch
- Download and Launch ELK Container: This downloads the ELK docker container and initializes it   with the specified ports being published

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 -10.0.0.4  
 -10.0.0.5    
 -10.0.0.6    
 -10.0.0.7    
 -10.1.0.4

We have installed the following Beats on these machines:
- Web-1, Web-2, Web-3

These Beats allow us to collect the following information from each machine:
- Filebeats collects system type events such as logins to see who is actively logging into the system.
- Metricbeats collects useful information such as cpu usage and memory, this is particularly useful when seeing if there are any aberant programs or behaviors accessing system resources.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/elk_install.yml
- Update the hosts file to include the attribute, such as [elk], then include your destination ip of the ELK server directly below
- Run the playbook, and navigate to http://[your_elk_server_ip]:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_/etc/ansible/filebeat-configuration.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? Edit the /etc/ansible/hosts file to add webserver/elkserver ip addresses
- _Which URL do you navigate to in order to check that the ELK server is running? http://168.62.211.128:5601/app/kibana#/home

Some useful commands:

Edit the hosts file in /etc/ansible and add the details from the screenshot and update your ip addresses.

Container persistance is important 
sudo docker start (container_ name) 
sudo docker attach (container_ name)

ping command is usefull to chack the web servers 
