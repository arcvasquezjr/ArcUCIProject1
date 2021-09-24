## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/Project1 Network Diagram.drawio.png)

These files have been tested and used to generate a live ELK deployment on AWS. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML files may be used to install only certain pieces of it, such as webservers-playbook.yml, elk-playbook.yml, filebeat-playbook.yml and metricbeat-playbook.yml.

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
A load balancer acts as a reverse proxy and distributes network or application traffic across a number of servers. Load balancers are used to increase capacity (concurrent users) and reliability of applications. They improve the overall performance of applications by decreasing the burden on servers associated with managing and maintaining application and network sessions, as well as by performing application-specific tasks.

Load balancers are generally grouped into two categories: Layer 4 and Layer 7. Layer 4 load balancers act upon data found in network and transport layer protocols (IP, TCP, FTP, UDP). Layer 7 load balancers distribute requests based upon data found in application layer protocols such as HTTP. The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. 

Jump box or jump server is a way to establish a clear funnel through which traffic passed to their infrastructure. The idea was simple: Designate one server as the control point and force administrator users to log into that system first. Once authenticated there, they could traverse to other servers without having to log in again.

This approach had numerous benefits, including ease of use after login, and aided organizations in meeting compliance regulations because they could provide straightforward audit logs. It also paralleled the way most organizations implemented identity and access management (IAM) across their environments. Jump servers, like Active Directory® domain controllers, allowed admins to establish a secure perimeter around IT resources. Once users were inside the perimeter, they faced fewer internal security measures. However, this approach also exposed organizations to enormous risks. Once a user — or a bad actor — breached the perimeter, they could traverse through the organization’s networks and resources with relative ease. But, that would not be part of this readme file.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the OS and system applications.
Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server, such as:
Apache, HAProxy, MongoDB, MySQL, Nginx, PostgreSQL, Redis, System, Zookeeper

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function  | IP Address     | Operating System |
|------------|-----------|----------------|------------------|
| Jump Box   | Gateway   | 172.31.9.197   | Amazon Linux     |
| Webserver1 | Web server| 172.31.3.214   | Amazon Linux     |
| Webserver2 | Web server| 172.31.16.110  | Amazon Linux     |
| ELK Server | ELK server| 172.31.30.8    | Ubuntu           |


### Access Policies

The machines on the internal network are not exposed to the public Internet. But, the test webpage being hosted can be accessed through the load balancer's DNS name WebserverLB-321323781.us-west-2.elb.amazonaws.com.

Only the Jumpbox machine can accept SSH connections from the Internet. Access to this machine is only allowed from the following IP addresses:
47.180.136.68/32

Machines within the network can only be accessed by Jumpbox like the Webserver1, Webserver2 and ELK server. 
At this time, only my local PC's on my network with WAN IP address 47.80.136.68/32 can access the ELK VM.

A summary of the access policies in place can be found in the table below.

| Name    	 | Publicly Accessible | Allowed IP Addresses |
|----------------|---------------------|----------------------|
| Jump Box       | No                  | 47.180.136.68/32     |
|Webserver1      | Yes                 | 0.0.0.0/0            |
|Webserver2      | Yes                 | 0.0.0.0/0            |
|Elk Server      | No                  | 47.180.136.68/32 and |
					 172.31.9.197/20

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. Ansible is an open-source software provisioning, configuration management, and application-deployment tool enabling infrastructure as code. It runs on many Unix-like systems, and can configure both Unix-like systems as well as Microsoft Windows.
No configuration was performed manually, which is advantageous because it reduces the possibility of human error.
Ansible works by connecting to your nodes and pushing out small programs, called modules to them. Modules are used to accomplish automation tasks.
These programs are written to be resource models of the desired state of the system. Ansible then executes these modules and removes them when finished.
Without modules, you’d have to rely on ad-hoc commands and scripting to accomplish tasks.

The playbook implements the following tasks:

.use the user name "ubuntu" for the installation
.increase the virtual memory 
.install python
.install docker
.download and launch a docker web container with the specified ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
(Images/docker_ps.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Webserver1 on private ip 172.31.3.214 and
Webserver2 on private IP 172.31.16.110

We have installed the following Beats on these machines:
Filebeat and Metricbeat to the two webservers.

These Beats allow us to collect the following information from each machine:
Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. When you start Filebeat, it starts one or more inputs that look in the locations you’ve specified for log data. For each log that Filebeat locates, Filebeat starts a harvester. Each harvester reads a single log for new content and sends the new log data to libbeat, which aggregates the events and sends the aggregated data to the output that you’ve configured for Filebeat.

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


### Using the Playbooks
In order to use the playbooks, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned, you can proceed to step I., otherwise continue with preparing an Ansible control node.

###Setting up a Docker Ansible Jumpbox control node

	- Copy the ArcOregon.pem file from your local to Jumpbox. If you have copied your key from previous activities, you can skip to the next step, otherwise from your local machine, using CMD, go to the folder where you 		  		have your key, for my case it is ArcOregon.pem under Downloads folder. 
		  	Use the command, scp -i "ArcOregon.pem" ArcOregon.pem ec2-172.31.9.197.us-west-2.compute.amazonaws.com:/home/ec2-user.

Installing Docker

		-SSH into the control node, for my case, it is the Jumpbox VM at my private IP 172.31.9.197 and follow the steps below: My prompt change to 
		ec2-user@172.31.9.197 ~}$ upon succesfull connection.

		-Install docker using the command,
			ec2-user@172.31.9.197 ~}$ sudo yum install amazon-linux-extras install docker -y
		
		-Start the docker service using the command,
			ec2-user@172.31.9.197 ~}$ sudo service docker start

		-To check the docker service status, use the command,
			ec2-user@172.31.9.197 ~}$ sudo service docker status	you should see it active (running)...

		-To avoid using the sudo command multiple times, use the usermod command to modify the docker group (add ec2-user to the docker group). For this to work you will need to disconnect your current SSH connection and 												reconnect, otherwise it won't work!
			ec2-user@172.31.9.197 ~}$ sudo usermod -a -G docker ec2-user

		-To check if Docker is installed, just use the command,
			ec2-user@172.31.9.197 ~}$ docker info

Installing Ansible
		
		Ansible is a tool to automate installing application on machines on a network.
		Run ansible on VM and use ansible to deploy applications to run services to run commands on destination machines.
		

	1.) Download Ansible
				ec2-user@172.31.9.197 ~}$ sudo docker pull cyberxsecurity/ansible

			To check downloaded image, use the command
				ec2-user@172.31.9.197 ~}$ docker images

					REPOSITORY		TAG	IMAGE ID	CREATED		SIZE
					webserver		V1	60fc85fee705	26 secs ago	321 MB
					centos			latest	300e3315adb2f	8 mos ago	209 MB
					cyberxsecurity/ansible	latest	7d2d9fa20ccf	3 mos ago	754 MB
			
			To delete an image, say centos, use the command;
				ec2-user@172.31.9.197 ~}$ docker rmi centos

	2.) Run Ansible 
				ec2-user@172.31.9.197 ~}$ docker run -t -i cyberxsecurity/ansible

					To run ansible and connect to the container, use the command;

						ec2-user@172.31.9.197 ~}$ docker run -t -i cyberxsecurity/ansible bash
							this will run the container and the bash part will connect us to the container, and this will bring up a different prompt

									root@d40e93b41f3a:~#

										To check if Ansible is already running, use the command;
										ansible, if the help appears, then it's already running
			
										Exit back to Docker.n To use Ansible, you need to have Ansible client, these are VMs that you are going to manage, install services, etc. Go ahead and 										create another VM instance in your VPC, if you don't have one yet.

	3.) List the containers by using the command,

				ec2-user@172.31.9.197 ~}$ sudo docker container list -a

					This will ist running containers like

						CONTAINER ID	IMAGES				COMMAND				CREATED		STATUS			PORTS
						9126fe65f1c1	cyberxsecurity/ansible		"/bin/sh -c /bin/bas.."		3 minutes ago	Exited(0) 2 mins ago	tender_montalcini	
						3213fcfa3b4e	webserver:v1			"/nginx -g 'daemon of..."	36 minutes ago	Exited(0) 36 mins ago	great_rhodes

						Look under PORTS and IMAGES to find out which container is running your Ansible server, so for this part, it is tender_montalcini

	3.) Start the container, say tender_montalcini

				ec2-user@172.31.9.197 ~}$ sudo docker start tender_montalcini

	4.) At this point, copy the key from Jumpbox docker to ansible container, using the format sudo docker cp <source file> <container id>:<destination location>

				ec2-user@172.31.9.197 ~}$ sudo docker cp ArcOregon.pem 9126fe65f1c1:/root

	5.) Then attach to the container, tender_montalcini

				ec2-user@172.31.9.197 ~}$ sudo docker attach tender_montalcini

	6.) Once connected to your Ansible container, your prompt will change to something like;

					root@d40e93b41f3a:~#			
		

	7.) Go to /etc/ansible directory

					root@d40e93b41f3a:~# cd /etc/ansible	


I.) Update the hosts file under /etc/ansible, to include

	[webservers]
	172.31.3.214 ansible_python_interpreter=/usr/bin/python3
	172.31.16.110 ansible_python_interpreter=/usr/bin/python3  
	[elk]
        172.31.30.8 ansible_python_interpreter=/usr/bin/python3

	using the command;
					root@d40e93b41f3a:~# nano hosts

II.) Update the filebeat-config.yml under /etc/ansible to include 172.31.30.8:9200 under Elasticsearch output, keeping the username: "elastic" and password to "changeme", and 172.31.30.8:5601 next to host: under setup.kibana.
					
					root@d40e93b41f3a:~# nano filebeat-config.yml

III.) Update metricbeat-config.yml under /etc/ansible to include 172.31.30.8:5601 under Kibana, Elasticsearch output and Logstash output.

					root@d40e93b41f3a:~# nano metricbeat-config.yml

IV.) Create a filebeat playbook, named it filebeat-playbook.yml. Paste the code below to it and save.

					root@d40e93b41f3a:~# nano filebeat-playbook.yml

---
- name: Installing and Launching Filebeat
  hosts: webservers
  remote_user: ec2-user
  become: yes
  tasks:
    # Use command module
  - name: Download filebeat .rpm file
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.8.1-x86_64.rpm
 
    # Use command module 
  - name: Install Filebeat .rpm
    command: rpm -vi filebeat-oss-7.8.1-x86_64.rpm

    # Use command module 
#  - name: Install Java 1.8 
#    command: yum install java-1.8.0-*
 
    # Use copy module
  - name: Drop in Filebeat.yml
    copy:
      src: /etc/ansible/filebeat-config.yml
      dest: /etc/filebeat/filebeat.yml

    # Use command module
  - name: Enable and Configure System Module
    command: sudo filebeat module enable system

    # Use command module 
  - name: Setup Filebeat
    command: sudo filebeat setup

    # Use command module
  - name: Start filebeat service
    command: sudo service filebeat start

    # Use command module
  - name: Enable service filebeat on boot
    systemd:
      name: filebeat
      enabled: yes


V.) Run the filebeat-playbook.yml;

				root@d40e93b41f3a:~# ansible-playbook -i hosts filebeat-playbook.yml --key-file ArcOregon.pem

					This will start installing Filebeat in the webservers.

VI.) Create a playbook and name it metricbeat-playbook.yml, paste the following code below and save it.

				root@d40e93b41f3a:~# nano metricbeat-playbook.yml

---
- name: Installing and Launch metricbeat
  hosts: webservers
  remote_user: ec2-user
  become: yes
  tasks:
    # Use command module
  - name: Download metricbeat .rpm file
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-x86_64.rpm
    # Use command module
  - name: Install metricbeat .rpm
    command: sudo rpm -vi metricbeat-7.6.1-x86_64.rpm
    # Use copy module
  - name: Drop in filebeat.yml
    copy:
      src: /etc/ansible/metricbeat-config.yml
      dest: /etc/metricbeat/metricbeat.yml
    # Use command module
  - name: Enable and Configure System Module
    command: sudo metricbeat modules enable docker
    # Use command module
  - name:  metricbeat setup
    command: sudo metricbeat setup
    # Use command module
  - name: Start metricbeat service
    command: sudo service metricbeat start
    # Use systemd module
  - name: Enable service metricbeat on boot
    systemd:
      name: metricbeat
      enabled: yes

VII.) Run the playbook metricbeat-playbook.yml;

				root@d40e93b41f3a:~# ansible-playbook -i hosts metricbeat-playbook.yml --key-file ArcOregon.pem

					This will start installing Metricbeat to the webservers.

VIII.) Open a browser and navigate to http://172.31.30.8:5601/app/kibana to check that the installation worked as expected.

VIX.) Adjust your security groups Inbound Rules, to prevent everybody from accessing your setup.
		For WebSrv-SG and ELK-SG Inbound Rules		Port Range		Source
					All ICMP-IPV4		All			0.0.0.0/0	
					SSH			22		 	My IP Adrress Only 47.180.136.68/32
					HTTP			80			My IP Adrress Only 47.180.136.68/32
					Custom TCP		5044			My IP Adrress Only 47.180.136.68/32
					Custom TCP		5601			My IP Adrress Only 47.180.136.68/32
					Custom TCP		9200			My IP Adrress Only 47.180.136.68/32

		
