# cysec-class
Files and project from class


## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

/Images/elkstack.drawio.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the instal-elk.yml file may be used to install only certain pieces of it, such as Filebeat.

  /Ansible/install-elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load balancers help in maintaining the integrity and availability of an application or network. A jump box allows the user to have on point of access of administrative tasks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
Filebeat monitors activity and collects records/logs of events.
Metriceat logs qunatitative metrics from the OS and other services running on the server.

The configuration details of each machine may be found below.

| Name          | Function          | IP       | OS    |
|---------------|-------------------|----------|-------|
| Jump-Box-Prov | Gateway           | 10.0.0.4 | Linux |
| Web-1         | Web Server - DVWA | 10.0.0.5 | Linux |
| Web-2         | Web Server - DVWA | 10.0.0.6 | Linux |
| ELK-VM        | Elk Stack         | 10.1.0.4 | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Prov machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP

Machines within the network can only be accessed by SSH.
The ELK-VM is only accessible from the Jump-Box-Prov, which requries a connection from my personal IP.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP       |
|---------------|---------------------|------------------|
| Jump-Box-Prov | No                  | Personal IP      |
| Web-1         | Through LB          | Jump40.122.28.34 |
| Web-2         | Through LB          | 40.122.28.34     |
| ELK-VM        | No                  | SSH 10.0.0.4     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
We can automate the installation process in order to deploy multiple servers easily and quickly without having to physically touch them.

The playbook implements the following tasks:

    Install Docker.io and pip3
    Increases VM memory
    Download and Configure elk docker container
    Sets Published Ports


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

/Images/dockerps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 - 10.0.0.5
Web-2 - 10.0.0.6

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat monitors activity and collects records/logs of events.
Metriceat logs qunatitative metrics from the OS and other services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files.
- Update the config files to include Private IP of the ELK-Server to the ElasticSearch and Kibana Sections of the Configuration File
- Run the playbook, and navigate to ELK-VMPIP:5601/app/kibana to check that the installation worked as expected.

-Which file is the playbook? install-elk.yml copy to /etc/ansible
-Which file do you update to make Ansible run the playbook on a specific machine? 
/etc/ansible/hosts.cfg
-How do I specify which machine to install the ELK server on versus which to install Filebeat on?
The host file has lines you can specify for this.
-Which URL do you navigate to in order to check that the ELK server is running?
http://mypublicip<ELK-VM-IP>:5601

