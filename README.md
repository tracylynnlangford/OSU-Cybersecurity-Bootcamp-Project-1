## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/47544604/160516628-4750841f-b563-41d5-9c13-53a425abdd93.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select playbooks may be used to install only certain portions, such as Filebeat.

[__Playbook files__](https://github.com/tracylynnlangford/OSU-Cybersecurity-Bootcamp-Project-1/tree/main/ansible)
  
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
- **__Filebeat__** - Allows for collection of log events (ie, failed login attempts, messages, warnings, errors) or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing
- **__Metricbeat__** - Collects metrics and statistics from the operating system (such as CPU load, memory data, network flow, etc. and ships them to the output that you specify, such as Elasticsearch or Logstash

**__Sample screen shot from Filebeat filtering for 'sample_web_logs'.__**
![image](https://user-images.githubusercontent.com/47544604/160513469-988af6fd-c01f-42b7-8ba2-98792bf127e2.png)

**__Sample screen shot from Metricbeat displays CPU metrics__**
![image](https://user-images.githubusercontent.com/47544604/160513960-7591cdd2-474f-48ec-bae3-ca4a061ae5c2.png)


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node (exists on the jump box in our drawing) already configured. Assuming you have such a control node provisioned: 

SSH into the Ansible container on the jump server and follow the steps below:
- Copy the playbook files from the [__ansible folder__](https://github.com/tracylynnlangford/OSU-Cybersecurity-Bootcamp-Project-1/tree/main/ansible) to /etc/ansible.
- Update the [hosts file](https://github.com/tracylynnlangford/OSU-Cybersecurity-Bootcamp-Project-1/blob/main/ansible/hosts.txt) to include a web group (Web1 & Web2) and an ELK group (ELK server)
- Run the playbook, and navigate to http://<external IP of ELK server>:5601/app/kibana to check that the installation worked as expected. Sample screen shot below:

![image](https://user-images.githubusercontent.com/47544604/160514677-f8dd8897-29b8-49b8-938e-1115ea4f07ef.png)


