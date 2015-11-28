In this repository I try to add necessary Ansible playbooks, templates and files in order to automatically deploy a two node Active-Passive
VoIP service using Kamailio and RTPProxy. Here I assumed that you authentication database lives on another host. My Linux distribution of choice
for this project is Debian Jessie.

In order to use the scripts you should install Ansible 2. Every other tool will be installed automatically. I separated the files for ease of development and use (or reuse in your own customizations). 
Description of each of the files is as follows:

settings.yml :      This file contains a bunch of variables that you can change to customize things like Kamailio's DBURL, Cluster's Virtual IP Address and so on.

kamailio.yml:       This file contains a few plays to compile and install Kamailio.

ha-tools.yml:       This file contains a play which installs Pacemaker and Corosync.

configure-ha.yml:   This file contains a play that configures necessary resources for Pacemaker.

mysql.yml:          This file contains a play that you can use to install and configure  MySQL server.

rtpproxy.yml:       This file contains two plays for installing and configuring a cluster of RTPProxy servers.

In order to deploy th cluster you should run the files in the following order:

Caution: Before starting make sure that the hostname of two nodes are different.

0- chmod a+x mysql.yml kamailio.yml ha-tools.yml configure-ha.yml rtpproxy.yml

1- Edit hosts file to add your hosts

2- Edit settings.yml to customize things like MySQL settings, IP addresses, ... Here if you want to have an Active-Passive cluster
with two nodes such that each node has a local RTPProxy server set withRTPProxyCluster to False (default setting). If you want to deploy 
a cluster of RTPProxy servers such that their settings is red from a MySQL server database set withRTPProxyCluster to True and configure 
other necessary variables.

3- Run mysql.yml to install your database server

4- Run kamailio.yml to install Kamailio

5- If you need a cluster of RTPProxy servers run rtpproxy.yml

6- Run ha-tools.yml to install HA tools

7- Run configure-ha.yml to configure HA tools


Author: Gholamreza Sabery Tabrizy

Email: reza_sabery_89@yahoo.com