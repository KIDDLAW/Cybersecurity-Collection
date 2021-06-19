## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.   

(Images/cloud_evironment.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  -filebeat-playbook.yml
 
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly stable, in addition to restricting traffic to the network.
Having load balancers ensures that a website is protected by spreading out the traffic amongst multiple servers. Having a jump box gives your environment security by only having one point of access. So instead of trying to harden multiple machines a person can put all their energy into making one incredibly difficult to crack.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system configuration.
- Filebeat watches for log data on your system. It also has the ability
  to slow down the traffic it is sending logstash so it doesn’t
  overburden it.    
- Metricbeat logs metrics on your system at a specific time.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    |  DVWA    | 10.0.0.5   | Linux            |
| Web-2    |  DVWA    | 10.0.0.6   | Linux            |
| Web-3    |  DVWA    | 10.0.0.7   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 76.103.236.71

Machines within the network can only be accessed by Ansible.
- Docker container 2df6a3f2cd82 172.17.0.2

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.5 10.0.0.6    |
|          |                     | 10.0.0.7 10.1.0.6    |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
once the automation is complete it is very easy to take down and relaunch the container.

The playbook implements the following tasks:
- It specifies the group of machines that this play will run on a well as the admin.
- The memory of the ELK machine is increased so that it will run properly.
- All of the necessary services (docker.io, pyhton3-pip, and docker) are installed.
- sebp/elk:761 is downloaded and ran
- The container is made to always start on boot.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.5
10.0.0.6
10.0.0.7
We have installed the following Beats on these machines:
- Filebeat
- Metricbeat
The configuration files for both of these beats can be found at 
(Beat_Config/Filebeat-config.yml)
(Beat_Config/Metricbeat-config.yml)

These Beats allow us to collect the following information from each machine:
- Filebeat collects log data of the system and forwards them to of elasticsearch. These logs could range from sudo commands to ssh.
- Metricbeat collects metrics over a specified period of time. These metrics could be users logged onto the web application.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible directory.
- Update the hosts file to include the ip address of the machine you wish to install the ELK server on. You are going to need to specify which group of hosts you are using with brackets []
- Run the playbook, and navigate to ip address:5601/app/kibana to check that the installation worked as expected.

Here are the commands that you would run to set up the ELK container.

Run the playbook: ansible-playbook install-elk.yml

Update hosts file: Sudo nano hosts

Update ansible.cfg file: Sudo nano ansible.cfg

Check if kibana is working on your server in the command line: 
curl localhost:5601/app/kibana (If you receive HTML then you have configured it correctly.)



