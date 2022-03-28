## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/tracylynnlangford/OSU-Cybersecurity-Bootcamp-Project-1/blob/116668774516c3de41511eeb95400aeedf10885d/diagrams/TracyLangfordWeek12_Homework.drawio.png "Logo Title Text 1")


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select playbooks may be used to install only certain portions, such as Filebeat.

- [install-elk.yml](../blob/master/ansible/install-elk.yml)
- [filebeat-playbook.yml](../blob/master/ansible/filebeat-playbook.yml)
- [metricbeat-playbook.yml](../blob/master/ansible/metricbeat-playbook.yml)
- [metricbeat-config.yml](../blob/master/ansible/metricbeat-config.yml)
- [filebeat-config.yml](../blob/master/ansible/filebeat-config.yml)
  
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the web application is highly available while also restricting access to the private network.
- Load balancers control network traffic and protect private networks using built-in network address translation (NAT). 
- The jump box is used by admins to connect to servers within the private network, avoiding direct connections to the          application servers.

Integrating an ELK server allows users to easily monitor the vulnerable web servers for changes to the logs and system resources. Software agents (beats) are installed on the Web servers to collect data:  
- The Filebeat agent monitors and harvests specified log events to be aggregated for output.
- Metricbeat collects statistics from server services and ships the data to a specified output.

The configuration details of each machine may be found below.


| Name           | Function                                                                                                      | IP Address                                 | Operating System                    |
|----------------|---------------------------------------------------------------------------------------------------------------|--------------------------------------------|-------------------------------------|
| JumpBoxRedTeam | Gateway  | Public: 20.25.27.214<br>Private: 10.0.0.5  | Ubuntu |
| Web1           | DVWA App | Public: 20.231.74.173<br>Private: 10.0.0.4 | Ubuntu |
| Web2           | DVWA App | Public: 20.231.74.173<br>Private: 10.0.0.6 | Ubuntu |
| Elk Server     | Kibana   | Public: 20.114.203.230<br>Private: 10.2.0.4 | Ubuntu |
| RedTeamLB | Load Balancing | Public: 20.231.74.173 | Basic Azure Load Balancer<br>Layer four |

### Access Policies

The servers on the internal network are not exposed to the public Internet. 

Only the jump box can accept connections from the Internet. Access to this machine is only allowed from the following IP address: 204.210.241.248:22. Servers within the private network can only be accessed by the jump box as well.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 204.210.241.248:22   |
| Web1     | No                  | 10.0.0.0/16          |
| Web2     | No                  | 10.0.0.0/16          |
| ElkServer| Yes                 | 204.210.241.248:5601 |

### Elk Configuration

Ansible was used to automate the ELK server setup. No configuration was performed manually, which is advantageous because it is simple to set up and use.  It can be used to configure many machines at once, and it can model complex workflows. 
The main advantage is a fast, secure setup process. 

The playbook implements the following tasks:
- Installs and configures Docker, Python and Kibana onto the ELK server
- Installs and configures Docker, Apache, Filebeat, Metricbeat on both web servers
- Installs and configures DVWA web application on both web servers

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![image](https://user-images.githubusercontent.com/47544604/160303171-270d5efb-6801-420c-9633-98a825956c60.png)

### Target Machines & Beats
This ELK server is configured to monitor the web servers (10.0.0.4 and 10.0.0.6).
We have installed the following Beats on these machines:
- Filebeat - Allows for collection of log events (ie, failed login attempts, messages, warnings, errors) or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing
- Metricbeat - Collects metrics and statistics from the operating system (such as CPU load, memory data, network flow, etc. and ships them to the output that you specify, such as Elasticsearch or Logstash


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node (exists on the jump box in our drawing) already configured. Assuming you have such a control node provisioned: 

SSH into the Ansible container on the jump server and follow the steps below:
- Copy the playbook files from the ansible folder on this repository (or create your own) to /etc/ansible.
- Update the [hosts file](../blob/master/ansible/hosts) to include a web group (Web1 & Web2) and an ELK group (ELK server)
- Run the playbook, and navigate to http://<external IP of ELK server>:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
