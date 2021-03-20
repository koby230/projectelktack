Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Cloud security](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  Enter the playbook file._ playbookelk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly regulated, in addition to restricting access to the network.
What aspect of security do load balancers protect? A load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider. 
What is the advantage of a jump box? 
The advantage of a jump-box is that any tools in place for the SAN system are maintained on that single system. Therefore, when an update to the SAN management software is available, only a single system requires the update.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the operating system and logs for each event.

What does Filebeat watch for? Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
 
What does Metricbeat record? Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web 1    | Gateway  | 10.0.0.5   | Linux            |
| Web 2    | Gateway  | 10.0.0.6   | Linux            |
| Web 3    | Gateway  | 10.0.0.7   | Linux            |

Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:


Machines within the network can only be accessed by Jumpbox.
Which machine did you allow to access your ELK VM? What was its IP address?
Jumpbox provisioner and its IP address was 13.93.230.70

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 10.0.0.1             |
|  Web 1   | no                  | 10.0.0.5             |
|  Web 2   | no                  | 10.0.0.6             |
|  Web 3   | no                  | 10.0.0.7             |

Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

What is the main advantage of automating configuration with Ansible? Advantage of using Ansible for Network Automation is the use of roles, When you write alot of playbooks often they tend to duplicate. 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ... Install Docker
- ... Ssh into containers
... Port 80 to localhost:5601
-The “hosts” file must be updated to reflect the name of the network and the IP addresses which are allowed to access the ELK stack:

>[webservers] 
>10.0.0.1 ansible_python_interpreter=/usr/bin/python3 
>10.0.0.5 ansible_python_interpreter=/usr/bin/python3 
>10.0.0.6 ansible_python_interpreter=/usr/bin/python3
>[elk] 
>10.0.0.7 ansible_python_interpreter=/usr/bin/python3

-Once the "hosts" file is updated, the ELK playbook must be made to tellt he computer which programs to automatically start: -In order to install and run the ELK playbook, the follwing command must be run on command line {ansible-playbook elkplaybook.yml}. After the command is run, the display will show which have been started, changed and/or failed.


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1-10.0.0.5, Web2-10.0.0.6, Web3-10.0.0.7

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
-Filebeat is a collection of data on log events. This information is sent through Logstash which outputs to Kibana and gives the ability to read what is happening within our network.

-Metricbeat is a shipper which will collect metric data from the operating system. It collects the stats and metrics to Logstash, or Elasticsearch, and the data can be read from the Kibana ouput.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- _Which file is the playbook? Where do you copy it? Attached to this Readme is a copy of the ansible playbook. This should be copied into a file on your ansible docker to the following location /etc/ansible/<file>

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? 

- The file which needs to be updated inside the ansible container is the hosts file. This must be updated (as seen at the beginning of this document) to reflect which private network IP addresses are allowed to host the ansible playbook. It is important to ssh into any machine of which the playbook is designed to run. Then copy the file and run it on that machine. ELK and Filebeat are designed to work together. For instance, the Filebeat program is designed to take logs and output them into Kibana via the ELK vm. Which means that the Filebeat should be installed on the web-machines where files are being monitored. A mirrored connection needs to be establisted through Azure so that no ssh connection is required from Web-machines to the ELK stack. This protects the ELK machine from attack. 

- _Which URL do you navigate to in order to check that the ELK server is running?
- In order to see if the ELK is running is this: http://<ELK_IP_52.--.--.--->:5601/app/kibana. If everything is working correctly, the Kibana page will appear right after. 


