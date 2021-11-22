Class Project-1, Elk Stack Deployment Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the file may be used to install only certain pieces of it, such as Filebeat.
  /etc/ansible/install-elk-playbook.yml
 
This document contains the following details:
Description of the Topology
Access Policies
ELK Configuration
Beats in Use
Machines Being Monitored
How to Use the Ansible Build
Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly efficient, in addition to restricting traffic to the network.
What aspect of security do load balancers protect?
Load balancers protect the system from DDoS attacks by shifting attack traffic.
Load Balancing contributes to the Availability aspect of security in regards to the CIA Triad.
What is the advantage of a jump box?
The advantage of a jump box is to give access to the user from a single node that can be secured and monitored.
The advantage of a JumpBox is the origination point for launching Administrative Tasks. This ultimately sets the JumpBox as a SAW (Secure Admin Workstation). All Administrators when conducting any Administrative Task will be required to connect to the JumpBox (SAW) before performing any task/assignment.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Logs and system traffic.
What does Filebeat watch for?
Filebeat watches for any information in the file system which has been changed and when it has.
Filebeat watches for log files/locations and collects log events
What does Metricbeat record?
Metricbeat takes the metrics and statistics that collects and ships them to the output you specify.
Metricbeat records metric and statistical data from the operating system and from services running on the server.
The configuration details of each machine may be found below.
Name
Function
IP Address
Operating System
JumpBox
Gateway
10.0.0.4
Linux(ubtntu 18.04)
Web-1
Server
10.0.0.5
Linux(ubtntu 18.04)
Web-2
Server
10.0.0.6
Linux(ubtntu 18.04)
Elk-VM1
Elk Server
10.1.0.4
Linux(ubtntu 18.04)

Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Add whitelisted IP addresses:- - Public IP address which changes every time when the VM is on/off eg of Public IP 137.135.115.14
Machines within the network can only be accessed by SSH.
Which machine did you allow to access your ELK VM? What was its IP address? JumpBox VM, its private Ip address(Vnet IP)-10.1.0.8
A summary of the access policies in place can be found in the table below.
Name
Publicly Accessible
Allowed IP Addresses
Jump Box
NO
10.1.0.8
Web-1
NO
10.1.0.9
Web-2
NO
10.1.0.10
Web-3
NO
10.1.0.11
Elk-VM1
NO
10.0.0.4

Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?
This allows you to deploy to multiple servers using a single playbook
The playbook implements the following tasks:
Install docker.io
Install Python-pip
Install docker container
Launch docker container: elk
Command: sysctl -w vm.max_map_count=262144
The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring:- - Web-1(10.0.0.5) Web-2(10.0.0.6)
We have installed the following Beats on these machines:
Specify which Beats you successfully installed:- - Filebeat - Metricbeat
These Beats allow us to collect the following information from each machine:
- Filebeat monitors log files or locations you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat collects metrics from the operating system and from services running on the server.
 
Using the Playbook-install-elk.yml
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
 
SSH into the control node and follow the steps below:
Copy the playbook file to /etc/ansible.
Update the configuration file to include the web servers and ElkVM (private Ip address.
Run the playbook, and navigate to ElkVM to check that the installation worked as expected. /etc/ansible/host should include:
[webservers] [10.1.0.9] ansible_python_interpreter=/usr/bin/python3 [10.1.0.10] ansible_python_interpreter=/usr/bin/python3 [10.1.0.11] ansible_python_interpreter=/usr/bin/python3
[elk] [10.1.0.4] ansible_python_interpreter=/usr/bin/python3
Run the playbook, and SSH into the Elk vm, then run docker ps to check that the installation worked as expected. Playbook: install_elk.yml Location: /etc/ansible/install_elk.yml Navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to confirm ELK and kibana are running. You may need to try from multiple web browsers Click 'Explore On Your Own' and you should see the following:

Answer the following questions to fill in the blanks:
Which file is the playbook? Where do you copy it? /etc/ansible/file/filebeat-configuration.yml
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ edit the /etc/ansible/hosts file to add webserver/elkserver ip addresses
Which URL do you navigate to in order to check that the ELK server is running? http://[your.ELK-VM.External.IP]:5601/app/kibana
