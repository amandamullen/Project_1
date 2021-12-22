# Elk Stack
# Automated Elk Stack Deployment

 The files in this repository were used to configure the network depicted below.   
    
![Alt text](Project_1/Project_1/Diagrams/Elk Stack Diagram.PNG/raw=true "Title") 
    
    These files have been tested and used to generate a live Elk Stack deployment on Azure. The files can be used to recreate the
    entire Elk Stack or just portions of the playbook file can be used to install files such as filebeat.

    (Ansible/install_elk_yml)

This document contains the following information:
 - Description of the Topology 
 - Access Policies
 - ELK Configuration
 - Beats in Use
 - Machines Being Monitored
 - How to Use the Ansible Build
 
***Description of the Topology
 
 There are two types of network topologies: physical and logical. Physical topology emphasizes the physical layout of the connected devices and nodes, while the logical topology focuses on the pattern of data transfer between network nodes.
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn vulnerable Web Application.
Regardless of whether it’s hardware or software, or what algorithm(s) it uses, a load balancer disburses traffic to different web servers in the
resource pool to ensure that no single server becomes overworked and subsequently unreliable. Load balancers effectively minimize server response 
time and maximize throughput.

What is the advantage of a jump box?
- A jump box is a secure computer that all admins first connect to before launching any administrative task or use as an origination point to connect to other servers or untrusted environments.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **filesystem** and system **resources / availability**.
- What does Filebeat watch for? **log files and filesystem changes**

The configuration details of each machine may be found below.
note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.7   |20.124.228.102 Linux 
| Web-1    | DVWA     | 10.0.0.4   |Linux            |
| Web-2    | DVWA     | 10.0.0.8   |Linux            |
| ELK-VM   | ELK Server | 10.1.0.4 |20.110.0.90 Linux

***Access Policies

The machines on the internal network are not exposed to the public Internet. 


Only the **JumpBox** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 **My home network public IP address (20.124.228.102)*
Machines within the network can only be accessed by SSH.

- Which machine did you allow to access your ELK VM? What was its IP address? JumpBox VM, its private Ip address(Vnet IP)10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes (SSH)           | SSH:My home network  |
| Web-1    | Yes (HTTP)          | HTTP:any, SSH:10.0.0.7   |
| Web-2    | Yes (HTTP)          | HTTP:any, SSH:10.0.0.7   |
| Web-3    | Yes (HTTP)          | HTTP:any, SSH:10.0.0.7   |
| ELK-VM   | Yes (HTTP, SSH)     | HTTP:any, SSH:10.0.0.7   |

*** Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is an advantage because...

- Easy to use and set up: No special coding skills are necessary to use Ansible’s playbooks.
- It's a free open-source tool.
- Powerful: Ansible lets you model even highly complex IT workflows. 
- Flexible: You can orchestrate and customize an entire application environment no matter where it’s deployed.
- Agentless: You will not need to install any other software, firewall ports or seperate management structures on the client systems you want to automate.
- Efficient: Because there is no extra software installed, there is more room for application resources on your server.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Downloads abd configures Elk Docker container
- Increase virtual memory
- Download and launch a docker
- Activates ports 5601, 9200, and 5044.




*** Target Machines & Beats
This ELK server is configured to monitor the following machines:
-Private IPs of Web-1 and Web-2

| Name      | IP Addresses         |
|---------- |----------------------|
| Web-1     | 10.0.0.4             |
| Web-2     | 10.0.0.8             |

We have installed the following Beat on these machines:

Filebeat

The Beat allows us to collect the following information from each machine:
- **Filebeat reads and forwards log files, and monitors file system changes.**

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:

Copy the playbook file to Ansible Control Node.
Playbook for Filebeat: [filebeat](Playbooks/filebeat-playbook.yml)
 
```
$ cd /etc/ansible
$ mkdir files
# Clone Repository + IaC Files
$ git clone https://github.com/name/Project-1-ELK-Stack-Project.git
# Move Playbooks and hosts file Into `/etc/ansible`
$ cp /Project-1-ELK-Stack-Project/ReadMe/Playbooks/*
```
- Update the hosts file to include webserver and elk
- Edit hosts file to update and to make Ansible run the playbook on a specific machine, and specify which machine to install the ELK server on versus which to install Filebeat.
- Copy of the hosts file is also here: hosts
```
$ cd /etc/ansible
$ cat > hosts <<EOF
[webservers]
10.0.0.4
10.0.0.8

[elk]
10.1.0.4
EOF
```
- Run the playbook, and navigate to Kibana (http://[Host IP]/app/kibana#/home) to check that the installation worked as expected.
```
cd /etc/ansible
 $ ansible-playbook install_elk.yml elk
 $ ansible-playbook install_filebeat.yml webservers
 
 ```
 - Check that the ELK server is running: http://[Host IP]/app/kibana#/home 

























