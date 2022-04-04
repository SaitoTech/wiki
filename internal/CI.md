---
title: Automated Deployment
description: 
published: true
date: 2022-03-01T10:54:55.222Z
tags: 
editor: markdown
dateCreated: 2022-02-03T08:30:45.705Z
---

# Automated Deployment Scripts


This document covers use of the automated deployment (ansible) scripts for updating and rebuilding various networks.

##  Current Networks

 * test (transient testing network)
 * staging (stable testing and demonstration environment)
 * production (production network - saito.io)
 
 
 ## Command and Control Server
 
 The command and control server is ```deployment.saito.network```
 
 ### Scripts
 
 All deployment scripts are run from the ```/root/deployment``` folder.
 
 The deployment script is ```./deploy```
 
#### Usage:
 
 ```./deploy``` ```action``` ```network``` ```[dev optional flag]``` ```-b|--branch=[branch]```
 |	```--branch``` option is only available on test network_ 
 
#### Example:
 
 ```./deploy nuke test dev```
 
This command runs the ```./compile nuke dev``` command on the test network.

### Details:

All commands are triggered by the one ```./deploy``` script.

Each network has a folder with a matching name in the root of the ```/deployment``` folder.

Actions:
 * nuke: 
   get latest code from git
   remove the chain and reset all configuration on all nodes
   recompile js client software
   start fresh
 
 * reset: 
   get latest code from git
   remove the chain and reset configuration but leave 'persistent' databases
   recompile js client software
   start fresh
 
 * restart: 
   get latest code from git
   recompile js client software
   restart nodes
 
 * compile:
   get latest code from git
   recompile js clients
 
 * other scripts perform tests and other actions

To see the available options for each network list the contents of the relevant directory.

## Permissions

ssh access to the deployment@saito.network C&C server is needed to operate the system. 


## Updates and management

Deployment scripts are managed under git.

The repository is at: https://github.com/SaitoTech/deployment

This is a private repository and deprecates the older 'ansible-setup' repository.

