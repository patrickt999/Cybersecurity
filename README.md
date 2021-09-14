## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![network diagram](https://user-images.githubusercontent.com/78185118/133347933-3f9898c7-30fc-43e2-ab78-d4f1d58eabd5.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the PLAYBOOK file may be used to install only certain pieces of it, such as Filebeat.


[install-elk.txt](https://github.com/patrickt999/Cybersecurity/files/6581426/install-elk.txt)
(elk_install.yml file)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly AVAILABLE, in addition to restricting REQUESTS to the network.
- _What aspect of security do load balancers protect?_<br/>
network infrastructure, application server availability<br/>
* _What is the advantage of a jump box?_<br/>
you can configure your jump box to run lightweight Docker containers that can be used to distribute software, versus having to install software directly on a host machine

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the LOGS and SYSTEM TRAFFIC.
- _What does Filebeat watch for?_<br/>
 logs, changes to the file system<br/>
* _What does Metricbeat record?_<br/>
aspects of a system that tell analysts about machine health

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Web server| 10.0.0.5  | Linux            |
| Web-2    | backup   | 10.0.0.6   | Linux            |
| ELK      | monitor  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JUMP BOX machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:<br/>
* _52.146.40.59_<br/>
Machines within the network can only be accessed by JUMP BOX.<br/>
* _Which machine did you allow to access your ELK VM? What was its IP address?_<br/>
Jump Box<br/>
ELKs public IP address is dynamic and its private IP is 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes     - 22         | my home IP           |
| DVWA     |  No                 | LB IP - 13.92.28.115 |
| LB       |  Yes    -   80       | *                    |
| ELK      |   Yes    -   5601    |  *                   |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...<br/>
* _What is the main advantage of automating configuration with Ansible?_<br/>
automating configuation with Ansible allows playbooks to be installed on multiple servers on a network with no manual configuration necessary

The playbook implements the following tasks:
- install services: apt module, docker.io and python3-pip
pip module, docker
- increase the memory: systemctl
- download and launch a docker elk container: docker_container module
- make sure that the docker service is started when the VM restarts: systemd module

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker_ps_output](https://user-images.githubusercontent.com/78185118/119436632-238ce880-bce2-11eb-81d4-ee42bc1b3299.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1
- Web-2

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:<br/>
_In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see._<br/>
* Filebeat: collects data about the file system, syslogs

* Metricbeat: collects machine metrics, CPU usage or inbound/outbound traffic

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/roles.
- Update the hosts file to include elk and the destination IP of the elk server
- Run the playbook, and navigate to http://[your.VM.ip]:5601/app/kibana to check that the installation worked as expected.
