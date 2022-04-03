# Project-I-ELK-Stack
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  - Project-I-ELK-Stack/Ansible/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting attacks to the network. Load balancers protect the availability aspect of security as it creates redundancy. As it distributes traffic evenly across servers, it ensures that no machine is overloaded and helps protect against DoS attacks.

Jumpboxes work as another layer of protection for the servers. The servers can only be accessed through the jumpbox, so this effectively creates a separation between the user and the servers making it less susceptible for a widespread attack. 


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat monitors log files, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
    Source: https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-overview.html#:~:text=Filebeat%20is%20a%20lightweight%20shipper,Elasticsearch%20or%20Logstash%20for%20indexing.
- Metricbeat records metrics and statistics from the system and services runing on the server and ships them to the output that you specify, such as Elasticsearch or Logstash.
    Source: https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-overview.html#:~:text=Metricbeat%20takes%20the%20metrics%20and,Apache


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Publicly Accessible | IP Address                              | Operating System |
|------------|---------------------|-----------------------------------------|------------------|
| Jump Box   | Gateway             | Public: 40.113.233.6  Private: 10.0.0.7 | Linux            |
| Web-1      | Server              | Public: 40.77.14.145 Private: 10.0.0.8  | Linux            |
| Web-2      | Server              | Public: 40.77.14.145 Private: 10.0.0.9  | Linux            |
| ELK-SERVER | Server              | Public: ELK-SERVER-ip Private: 10.1.0.4 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 10.0.0.8
- 10.0.0.9

Machines within the network can only be accessed by the ELK Virtual Machine.
- I allowed the Jump Box Provisioner access to the ELK VM. Its IP is 10.0.0.7.

A summary of the access policies in place can be found in the table below.

| Name                | Publicly Accessible | Allowed IP Addresses  |
|---------------------|---------------------|-----------------------|
| JumpBox Provisioner |         Yes         | Public: 40.113.233.6  |
| Web-1               |          No         | Private: 10.1.0.4     |
| Web-2               |          No         | Private: 10.1.0.4     |
| ELK-SERVER          |          No         | Private: 10.1.0.4     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- of its ease of use and efficiency. It is easy to set up, and can handle multiple or complex configurations, while making it easy for the user to set up because its language is English-like.

The playbook implements the following tasks:
- Installs services like docker.io and python3-pip
- Increases virtual memory
- Enables service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!https://github.com/athenavalero/Project-I-ELK-Stack/blob/main/Linux/elk.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 : 10.0.0.8
- Web-2 : 10.0.0.9
- ELK-SERVER: 10.1.0.4

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeats collects data about log events whereas Metricbeats records metrics and statistics. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook (.yml) file to the Ansible directory.
- Update the host file to include the webserver and ELK server...
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
   The playbook is usually denoted by a .yml extension since it's a YAML file. It is copied to the etc/ansible/ directory.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
   To make Ansible run the playbook on a specific machine, the etc/ansible/hosts file is updated. To specify which machine to install the ELK server on versus to install Filebeat on, the config file must be updated.
- _Which URL do you navigate to in order to check that the ELK server is running?
- http://[ELK-VM.External.IP]:5601/app/kibana

