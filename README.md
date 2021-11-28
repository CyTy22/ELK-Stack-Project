## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
<img width="728" alt="Network Diagram" src="https://user-images.githubusercontent.com/86851214/143726686-9fa1f858-33df-47c3-a6ce-25d391f306e7.png">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  
/etc/ansible/install-elk-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorized access to the network. Load Balancing plays an important security role as computing moves evermore to the cloud. The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider. 

A jump box is a secure computer that all admins first connect to before launching any administrative task or use as an origination point to connect to other servers or untrusted environments.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

What does Filebeat watch for?
Filebeat watches for log files/locations and collects events related to any files changed. 

What does Metricbeat record?
Metricbeat records metrics and statistical data from the operating system and services that are running on the server.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.6   | Linux            |
| Web-1    |Web Server| 10.0.0.4   | Linux            |
| Web-2    |Web Server| 10.0.0.5   | Linux            |
| Web-3    |Web Server| 10.0.0.8   | Linux            |
| Elk Stack|Elk Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: My personal IP Address

Machines within the network can only be accessed by SSH.
The Elk is only accessible through successful SSH from the Jumpbox.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My Personal IP       |
| Web-1    | No                  | 10.0.0.6             |
| Web-2    | No                  | 10.0.0.6             |  
| Web-3    | No                  | 10.0.0.6             |
| Elk      | No                  | 10.0.0.6             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because you can deploy several severs quickly through the run of a playbook.

The playbook implements the following tasks:
.Configures the machine with Docker
.Installs Docker.io and pip3
.Utilize more memory
.Download and Run Docker Elk Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![elk_docker](https://user-images.githubusercontent.com/86851214/143726706-1a1bd39d-58d1-4901-8a8e-0dfc63acb79c.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

Web-1 10.0.0.4
Web-2 10.0.0.5
Web-3 10.0.0.8

We have installed the following Beats on these machines:

Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat watches for log files/locations and collects events related to any files changed

Metricbeat records metrics and statistical data from the operating system and services that are running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install_elk.yml file to /etc/ansible
- Update the host file to include the private IP addresses of Web 1-3 and Elk Server with python 3 interpreter
- Run the playbook, and navigate to Elk server to check that the installation worked as expected.

Answer the following questions to fill in the blanks:
Which file is the playbook? Where do you copy it?
/etc/ansible/file/filebeat-configuration.yml

Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
nano (edit) /etc/ansible/hosts file to add the elk server's IP address

Which URL do you navigate to in order to check that the ELK server is running?

http://[your.ELK-VM.External.IP]:5601/app/kibana
<img width="960" alt="Kibana Home" src="https://user-images.githubusercontent.com/86851214/143776025-5f15468a-3118-4302-8248-0ed403e1acfd.png">

Answer the following questions to fill in the blanks:

Which file is the playbook? Where do you copy it? /etc/ansible/file/filebeat-configuration.yml
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ edit the /etc/ansible/hosts file to add webserver/elkserver ip addresses
Which URL do you navigate to in order to check that the ELK server is running? http://[your.ELK-VM.External.IP]:5601/app/kibana
Using the Playbook-filebeat-playbook.yml

Copy the filebeat.yml file to the /etc/ansible/files/ directory.

Update the configuration file to include the Private IP of the Elk-Server to the ElasticSearch and Kibana sections of the configuration file.

Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the filebeat setup, and start the filebeat service.

Create a new playbook in the /etc/ansible/roles/ directory that will install, drop in the updated configuration file, enable and configure system module, run the metricbeat setup, and start the metricbeat service.

Run the playbooks, and navigate back to the installation page on the ELk-Server GUI, click the check data on the Module Status

Click the verfiy incoming Data to check and see the receiving logs from the DVWA machines.

you should see the following:
<img width="960" alt="Filebeat Logs" src="https://user-images.githubusercontent.com/86851214/143776321-605873f0-c1b7-471f-8d73-e60ce8c17198.png">

The commands needed to run the Ansible configuration for the Elk-Server are:

ssh sysadmin@JumpBox(Public IP)
sudo docker container list -a (locate your ansible container)
sudo docker start container (name of the container)
sudo docker attach container (name of the container)
cd /etc/ansible/ - ansible-playbook elk.yml (configures Elk-Server and starts the Elk container on the Elk-Server) wait a couple minutes for the implementation of the Elk-Server - cd /etc/ansible/roles/ - ansible-playbook filebeat-playbook.yml (installs Filebeat and Metricbeat) - open a new web browser (http://[your.ELK-VM.External.IP]:5601/app/kibana) This will bring up the Kibana Web Portal - check the Module status for file beat and metric beat to see their data receiving.
