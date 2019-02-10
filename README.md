Kamailio-HA
===========

This repository contains necessary Ansible playbooks, templates and files for automatic deployment of one of the
following scenarios:

* A two node Active-Passive Kamailio Cluster with a local RTPProxy instance
* A two node Active-Passive Kamailio Cluster with a cluster of RTPProxy servers

**Caution**: The current version is updated to work on *Debian Stretch*. The previous version works on *Debian Jessie*.

Contents
========

**settings.yml** :      This file contains a bunch of variables that you can change to customize things like Kamailio's 
DBURL, Cluster's Virtual IP Address and so on.

**kamailio.yml**:       This file contains a few plays to compile and install Kamailio.

**ha-tools.yml**:       This file contains a play which installs Pacemaker and Corosync.

**configure-ha.yml**:   This file contains a play that configures necessary resources for Pacemaker.

**mysql.yml**:          This file contains a play that you can use to install and configure  MySQL server.

**rtpproxy.yml**:       This file contains two plays for installing and configuring a cluster of RTPProxy servers.

**Docker-related files**: You can use these files to setup a test environment for Ansible playbooks.

1. AnsibleMachine.df:   Dockerfile to create a container with the latest version of Ansible installed. You can use this
machine to run Ansible playbooks.

2. TargetMachine.df: Dockerfile to create a container with Debian Stretch and an SSH server. This Dockerfile can be used
to create target machines (machines that Ansible will deploy software on them).

3. docker-compose.yml: This file uses AnsibleMachine.df and TargetMachine.df Dockerfiles to set-up a test environment for
Ansible playbooks.


Test using docker-compose
=========================
You can use docker-compose to setup a multi-container environment with a bridged network in order to test the playbooks.
The docker-compose.yml with Dockerfiles can also help you in setting up your real operational environment. In order to
run Ansible playbooks follow these steps:

0. Install Docker and docker-compose:
    * How to install Docker on Debian:https://docs.docker.com/install/linux/docker-ce/debian/
    * How to install docker-compose on Debian: https://docs.docker.com/compose/install/
    
1. Change your current directory to the directory of the project and run the following command:

    `# docker-compose up -d` 

2. Use the following command to run a specific Ansible playbook:

    `# docker exec ansible-machine ansible-playbook -i hosts <playbook.yml>`

Using without Docker
=============
If you do not want to use Docker, you should generally have two types of machines:

1. A deployment machine with Ansible. This machine should satisfy these prerequisites: 

    * Debian Stretch (Debian 9)
    * The latest version of Ansible
    * sshpass : apt-get install sshpass
    
2. A bunch of target machines (machines that Ansible will deploy on them). These machines should have:
    * Python
    * SSH server
    
Now copy the project on the deployment machine, and refer to the **Usage** section.


Usage
=====

**Caution**: Before starting make sure that the hostname of two nodes are different.

**0**- chmod a+x mysql.yml kamailio.yml ha-tools.yml configure-ha.yml rtpproxy.yml

**1**- Edit hosts file to add your hosts

**2**- Edit settings.yml to customize things like MySQL settings, IP addresses, ... Here if you want to have an Active-Passive cluster
with two nodes such that each node has a local RTPProxy server set withRTPProxyCluster to False (default setting). If you want to deploy 
a cluster of RTPProxy servers such that their settings is red from a MySQL server database set withRTPProxyCluster to True and configure 
other necessary variables.

**3**- Run mysql.yml to install your database server

**4**- Run kamailio.yml to install Kamailio

**5**- If you need a cluster of RTPProxy servers run rtpproxy.yml

**6**- Run ha-tools.yml to install HA tools

**7**- Run configure-ha.yml to configure HA tools

Authors
=======

**Author**: Gholamreza Sabery Tabrizy

**Email**: reza_sabery_89@yahoo.com