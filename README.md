## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Cloud-Diagram](/diagrams/Cloud-Diagram.svg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible folder may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider. A jump box is a secure computer that all admins first connect to before launching any administrative task or use as an origination point to connect to other servers or untrusted environments.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

- Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as: Apache.

The configuration details of each machine may be found below.

| Name          | Function   | Public IP     | Private IP                         | Operating System |
|---------------|------------|---------------|------------------------------------|------------------|
| Jump-Box      | Gateway    | Create IP     | 10.0.01                            | Linux Server     |
| Web-1         | Web Server | Load Balancer | 10.0.0.4                           | Linux Server     |
| Web-2         | Web Server | Load Balancer | 10.0.0.5                           | Linux Server     |
| Web-3         | Web Server | Load Balancer | 10.0.0.6                           | Linux Server     |
| Load Balancer | Web Server | Front End IP  | Backend Pool (Web-1, Web-2, Web-3) |                  |
| ELK-Server    | Monitoring | Create IP     | 10.0.0.8                           | Linux Server     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 

Machines within the network can only be accessed by the Jump-Box machine.

A summary of the access policies in place can be found in the table below.

| Name        | Publicly Accesible | Allowed IP Addresses |
|-------------|--------------------|----------------------|
| Jump-Box    | Yes                | All Private IPs      |
| ELK-Server  | Yes                | HTTP port 5601       |
| Web Servers | Yes                | HTTP                 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible automates provisioning, configuration management, application deployment, orchestration, and many other IT processes.

The playbook implements the following tasks:
- Takes the remote_user variable in ansible.cfg and uses it through the automatiion
- Installs Docker
- Installs package manager for Python3 (pip3)
- Downloads, Installs and Enables a Docker ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Output](/ansible/images/docker_ps_output.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.4
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files or locations that are specified by the user, collects log events and forwards them either to Elastisearch or Logstash for indexing
- Metricbeat collect metric data from your target servers, monitors other beats and ELK stack itself.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the pentest file to /etc/ansible.
- Update the ansible.cfg and hosts file to include the webserver and ELK server Private IPs. 
- Run the playbook, and navigate to http://elk-server's-public-IP:5601 to check that the installation worked as expected.
