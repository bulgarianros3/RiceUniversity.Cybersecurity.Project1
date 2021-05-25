## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![network diagram](https://github.com/bulgarianros3/RiceUniversity.Cybersecurity.Project1/blob/main/Diagrams/Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook (.yml) files may be used to install only certain pieces of it, such as Filebeat.
- [myfirstplaybook.yml](https://github.com/bulgarianros3/RiceUniversity.Cybersecurity.Project1/blob/main/Ansible/myfirstplaybook.yml)
- [instal-elk.yml](https://github.com/bulgarianros3/RiceUniversity.Cybersecurity.Project1/blob/main/Ansible/install-elk.yml)
- [metricbeat-install.yml](https://github.com/bulgarianros3/RiceUniversity.Cybersecurity.Project1/blob/main/Ansible/metricbeat-install.yml)
- [filebeat-playbook.yml](https://github.com/bulgarianros3/RiceUniversity.Cybersecurity.Project1/blob/main/Ansible/filebeat-playbook.yml)


This document contains the following details:
-  Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. In regards to the CIA triad, load balancing takes part of the availability aspect of security becuase that's exactly what it ensures to the webservers: availability. The advantage of having a jump box is that you have one origin point for administrative tasks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- Filebeat watches for log files/locations and collects log events.
- Metricbeat records metrics and statistical data from the operating system and from services running on the server.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux (ubuntu 18.04) |
| Web-1    | DVWA Container | 10.0.0.6 | Linux (ubuntu 18.04) |
| Web-2    | DVWA Container | 10.0.0.7 | Linux (ubuntu 18.04)|
| ELK.server| ELK Stack | 10.1.0.5 | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My Personal IP Address

Machines within the network can only be accessed by SSH.
- The ELK.server is only accessible by SSH from the Jump Box at IP 10.0.0.4 and via web access from my personal IP Address.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.4 and Personal IP   |
| Web-1    | No                  | 10.0.0.4       |
| Web-2    | No                  | 10.0.0.4            |
| ELK.server | Yes               | 10.0.0.4 and Personal IP   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Allows for a consistent configuration. You can deploy multiple servers easily and quickly.

The playbook implements the following tasks:
- Install 'docker.io' and 'python3-pip' packages with 'apt' module
- Install docker 'python' package with 'pip'
- Increase memory with 'sysctl' module
- Enable 'systemd' docker service
- Run ELK docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker.ps](https://github.com/bulgarianros3/RiceUniversity.Cybersecurity.Project1/blob/main/Diagrams/Screen%20Shot%202021-05-24%20at%209.23.26%20PM.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.6
- Web-2: 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as: Apache. HAProxy.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml playbook file to /etc/ansible/roles/ directory inside the ansible container.
- Update the configuration files to include the Private IP of the ELK-Server to the ElasticSearch and Kibana Sections of the Configuration File
- Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.


