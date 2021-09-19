## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/Project1 Network Diagram)

These files have been tested and used to generate a live ELK deployment on AWS. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
A load balancer acts as a reverse proxy and distributes network or application traffic across a number of servers. Load balancers are used to increase capacity (concurrent users) and reliability of applications. They improve the overall performance of applications by decreasing the burden on servers associated with managing and maintaining application and network sessions, as well as by performing application-specific tasks.

Load balancers are generally grouped into two categories: Layer 4 and Layer 7. Layer 4 load balancers act upon data found in network and transport layer protocols (IP, TCP, FTP, UDP). Layer 7 load balancers distribute requests based upon data found in application layer protocols such as HTTP.

The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. Jump box or jump server is a way to establish a clear funnel through which traffic passed to their infrastructure. The idea was simple: Designate one server as the control point and force users to log into that system first. Once authenticated there, they could traverse to other servers without having to log in again.

This approach had numerous benefits, including ease of use after login, and aided organizations in meeting compliance regulations because they could provide straightforward audit logs. It also paralleled the way most organizations implemented identity and access management (IAM) across their environments. Jump servers, like Active Directory® domain controllers, allowed admins to establish a secure perimeter around IT resources. Once users were inside the perimeter, they faced fewer internal security measures.

However, this approach also exposed organizations to enormous risks. Once a user — or a bad actor — breached the perimeter, they could traverse through the organization’s networks and resources with relative ease. But, that would not be part of this readme file.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the OS and system applications.
Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as:

Apache
HAProxy
MongoDB
MySQL
Nginx
PostgreSQL
Redis
System
Zookeeper

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function  | IP Address     | Operating System |
|------------|-----------|----------------|------------------|
| Jump Box   | Gateway   | 172.31.9.197   | Amazon Linux     |
| Webserver1 | Web server| 172.31.3.214   | Amazon Linux     |
| Webserver2 | Web server| 172.31.16.110  | Amazon Linux     |
| ELK Server | ELK server| 172.31.30.8    | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
47.180.136.68/32

Machines within the network can only be accessed by Jumpbox.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 47.180.136.68/32     |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. Ansible is an open-source software provisioning, configuration management, and application-deployment tool enabling infrastructure as code. It runs on many Unix-like systems, and can configure both Unix-like systems as well as Microsoft Windows.
No configuration was performed manually, which is advantageous because it reduces the possibility of human error.
Ansible works by connecting to your nodes and pushing out small programs, called modules to them. Modules are used to accomplish automation tasks.
These programs are written to be resource models of the desired state of the system. Ansible then executes these modules and removes them when finished.
Without modules, you’d have to rely on ad-hoc commands and scripting to accomplish tasks.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._