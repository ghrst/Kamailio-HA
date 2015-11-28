Kamailio-HA
===========

This repository contains necessary Ansible playbooks, templates and files for automatic deployment of one of the following scenarios:

* A two node Active-Passive Kamailio Cluster with a local RTPProxy instance
* A two node Active-Passive Kamailio Cluster with a cluster of RTPProxy servers

**Caution**: These script are written for usage on *Debian Jessie*.

Contents
========

**settings.yml** :      This file contains a bunch of variables that you can change to customize things like Kamailio's DBURL, Cluster's Virtual IP Address and so on.

**kamailio.yml**:       This file contains a few plays to compile and install Kamailio.

**ha-tools.yml**:       This file contains a play which installs Pacemaker and Corosync.

**configure-ha.yml**:   This file contains a play that configures necessary resources for Pacemaker.

**mysql.yml**:          This file contains a play that you can use to install and configure  MySQL server.

**rtpproxy.yml**:       This file contains two plays for installing and configuring a cluster of RTPProxy servers.


Prerequisites
=============

* Debian Jessie
* Ansible 2


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