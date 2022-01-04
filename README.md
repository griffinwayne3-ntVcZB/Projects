## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

/Diagrams/Cloud_Network_Diagram.PNG

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  /ansible/filebeat.yml

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
- Load balancers protect against things like DDoS attacks, so the aspect of security it protects would be availability, so ensure it is up and available for others as often as possible. The advantage of using a jump box is that it a secure computer that admins can first connect to before launching administrative tasks or they can be used to connect to other servers or untrusted environments with safer access

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- Filebeat monitors and records logs from the virtual machines Web 1 and Web 2.
- Metricbeat records the metrics and statistics that it collects from the virtual machines Web 1 and Web 2.

The configuration details of each machine may be found below.

| Name     | Function       | IP Address   | Operating System |
|----------|----------------|--------------|------------------|
| Jump Box | Gateway        | 20.124.218.79| Linux            |
| Web 1    | Virtual Machine| 10.0.0.5     | Linux            |
| Web 2    | Virtual Machine| 10.0.0.6     | Linux            |
| Elk      | Elk Stack      | 10.1.0.4     | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Host Public IP

Machines within the network can only be accessed by SSHing into the machines with the Jump Box virtual machine.
- I allowed my Jump Box to allow access to my ELK VM. It's IP is 20.124.218.79.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses             |
|----------|---------------------|----------------------------------|
| Jump Box | NO                  | Host Public IP                   |
| Web 1    | NO                  | 20.124.218.79                    |
| Web 2    | NO                  | 20.124.218.79                    |
| ELK      | NO                  | 20.124.218.79 and Host Public IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage is that you can use YAML Playbooks to install and setup multiple programs on your VMs all while saving time not having to install things on your VMs one by one.

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install Docker module
- Increase virtual memory
- Use more memory
- download and launch a docker elk container
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- The IPs of the machines being monitored are Web 1: 10.0.0.5 and Web 2: 10.0.0.6

We have installed the following Beats on these machines:
- We installed Filebeat and Metricbeat.

These Beats allow us to collect the following information from each machine:
- Filebeat monitors log files or locations you specify and sends a copy to Logstash or Elasticsearch. Metricbeat records metrics and statistics and also sends a copy to Logstash or Elasticsearch. This shows metrics and data from services on the VM.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yaml playbook file to /etc/ansible in the container.
- Update the hosts file to include the IP addresses of the VMs you're running the yaml playbooks onto.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

- The playbook file is the file with the .yml extension on it. You would copy this file into the /etc/ansible directory in your container.
- The file you would update would be the hosts file in the ansible container. You would add the private IP addresses of your VMs. You can specify which machines you want to install things using the playbook by adding a specialized sections in the hosts file. We created one called webservers and chose which VMs we were going to be a part of that specific group, and then you can use the webservers name to install the files onto specific machines instead of using the VMs' IPs. 
- http//:13.77.212.100:5601/app/kibana  (13.77.212.100 is the ELK VM public IP)