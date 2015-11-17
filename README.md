In this repository I try to add necessary Ansible playbooks, templates and files in order to automatically deploy a two node Active-Passive
VoIP service using Kamailio and RTPProxy. Here I assumed that you authentication database lives on another host. My Linux distribution of choice
for this project is Debian Jessie.

In order to use the scripts you should install Ansible 2. Every other tool will be installed automatically. Currently we have 3 main
playbooks in the repository. Each playbook contains a single play. I separated the files at the beginning for ease of development but 
in future there may be merged together. Description of each of the files is as follows:

settings.yml :      This file contains a bunch of variables that you can change to customize things like Kamailio's DBURL, Cluster's Virtual IP Address and so on.

kamailio.yml:       This file contains a play to compile and install Kamailio.

ha-tools.yml:       This file contains a play which installs Pacemaker and Corosync.

configure-ha.yml:   This file contains a play that configures necessary resources for Pacemaker.

mysql.yml:          This file contains a play that you can use to install and configure  MySQL server.

In order to deploy th cluster you should run the files in the following order:

0- chmod a+x mysql.yml kamailio.yml ha-tools.yml configure-ha.yml

1- Edit hosts file to add your hosts

2- Edit settings.yml to customize things like MySQL settings, IP addresses, ...

3- Run mysql.yml to install your database server

4- Run kamailio.yml to install Kamailio

5- Run ha-tools.yml to install HA tools

6- Run configure-ha.yml to configure HA tools

Author: Gholamreza Sabery Tabrizy

Email: reza_sabery_89@yahoo.com