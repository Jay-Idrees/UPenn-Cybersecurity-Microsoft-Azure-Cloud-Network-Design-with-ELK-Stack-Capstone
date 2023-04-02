
# UPenn CyberSecurity Capstone

![](cloud_network_Idrees.png)

### Contact: 

Jay J. Idrees, M.D., M.P.H., S.Eng., C.E.H <br />
Full-Stack Software Engineer<br />
[Jay-Idrees](https://github.com/Jay-Idrees) ![Github](http://img.shields.io/badge/github-black?style=flat&logo=github)<br />

E-mail: Dr.Idrees@MedicalMarijuana.Expert

###   Automated ELK Stack Deployment
---
The files in this repository were used to configure the network depicted above.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions used to install only certain pieces of it, such as Filebeat or Metricbeat.

- **[install-filebeat.yml](Scripts/install-filebeat.yml)**
- **[install-metricbeat.yml](Scripts/install-metricbeat.yml)**
- **[install-elk.yml](Scripts/install-elk.yml)**

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology
---
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA (D*mn Vulnerable Web Application)

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

> **Load balancing** is the process of distributing incoming reequests/tasks over a set of resources in order to prevent disproportionate skew of requests load towards one specific server. For example, this can be particularly useful in maintaining availability of services to customers in the setting of a DoS attack on one of the server, rendering it unavailable. If the same services are available on an alternate server, the load balancer can distribute the web traffic to the alternate server when the primary server is 'overloaded' - this way the services (such as sales) continue to remain operational even in the mist of the attack. In addition it can also be configured to limit access to particular servers to prevent penetration by hackers. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files, logs and system metrics.

> **Filebeat** collects data about the file system. It is helpful in detecting changes to certain important files stampd by time like for example if a hacker attemps to change etc/passwd and this information is then sent to Elasticsearch on the ELK Server

> **Metricbeat** Collects metrics to help with the assessment regarding the operational state of computer machines on the network (VMs in this case) and then sends it to Elasticsearch on ELK Server. For example it can be helpful in determining CPU usage, memory disk I/O, Network I/O and Uptime information. 

The configuration details of each machine may be found below.


| Name     | Function     | IP Address | Operating System |
|----------|--------------|------------|------------------|
| Jump-Box | Gateway      | 10.0.0.4   |    Linux         |
| Web-1    | Server       | 10.0.0.5   |    Linux         |
| Web-2    | Server       | 10.0.0.6   |    Linux         |                  
| Web-3    | Server       | 10.0.0.7   |    Linux         |                  
| ELK      | Monitoring   | 10.1.0.4   |    Linux         |


### Access Policies
---
The machines on the internal network are not exposed to the public Internet. 

Only the **Jump-box** machine can accept connections from the Internet. Access to this machine is only allowed from the designiated Admin IP address via SSH

Machines within the network can only be accessed by **Jump-Box**.
- Only the Jump-Box can connect to it and its IP is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses         |
|----------|---------------------|------------------------------|
| Jump-Box |     Yes             | Admin's IP address via ssh   |
| Web-1    |     No, Only via JB | 10.0.0.1-254                 |
| Web-2    |     No, Only via JB | 10.0.0.1-254                 |
| Web-3    |     No, Only via JB | 10.0.0.1-254                 |
| ELK      |     No, Only via JB | 10.0.0.1-254                 |



### Elk Configuration
---
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because:

 > It simplifies the process of configuring additional machines or updating changes to all existing ones to the network simultaneously. We will only have to make changes to the ansible playbook and it will automatically be implemented to all the machines linked with the playbook. Alternatively if we do not use the playbook then we will have to make configuration changes to all of the machines individually which can be cumbersome and error prone

The playbook implements the following tasks:

- Installs Docker, which intern facilitates instalation of containers
- Installs Python-pip
- Installs Docker python module
- Increases virtual memory
- Downloads and launches a docker ELK container with the ports `5601`, `9200`, `5044`

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](Docker-ps.png)


### Target Machines & Beats
---
This ELK server is configured to monitor the following machines on which `filebeat` and `metricbeat` are installed:
- Web-1
- Web-2
- Web-3

We have installed the following Beats on these machines:
- `filebeat`
- `metricbeat`

These Beats allow us to collect the following information from each machine:

> **Filebeat** collects data about the file system. Helpful in detecting changes to certain important files stampd by time like for example if a hacker attemps to chenge etc/passwd and this information is then sent to Elasticsearch on the ELK Server

> **Metcicbeat** Collects metrics to help with the assessment about the operational state of computer machines on the network (VMs in this case) and then sends it to Elasticsearch on ELK For example it can be helpful in determining CPU usage, memory sisk IO, Network UO and Uptime information. 

### Using the Playbook
---

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the  **`install-elk.yml`** file to Ansible container folder **`/etc/ansible/files/`**
- Update the hosts file **`/etc/ansible/hosts`** to include **`ELK server IP address: 10.1.0.4`**
- Run the playbook **`install-elk.yml`**, and navigate to **`/etc/ansible/http://<VM IP>/:5601`** to check that the installation worked as expected.
- The playbook file is **`install-elk.yml`** and its copied in **`/etc/ansible`**
- Updating the host file will make Ansible run the playbook on a specific machine 
- By adding a private IP under "servers" you can specify which machine to install and the ELK server on vs filebeat
- The URL to navigate to in order to check ELK server **`<VM IP>.49:5601`**

