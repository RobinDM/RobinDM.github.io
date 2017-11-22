# Get Started, Part 1: Orientation and setup

## Prerequisites

We need to assume you are familiar with a few concepts before we begin.

 - IP Addresses and Ports
 - Virtual Machines
 - Editing configuration files
 - Basic familiarity with the ideas of code dependencies and  
   building
 - Machine resource usage terms, like CPU percentages, RAM use  
   in bytes, etc.

## A brief explanation of containers

An image is lightweight, stand-alone, executable package that includes everything needed to run a piece of software, including the code, a runtime, libraries, environment variables, and config files.

A container is a runtime instance of an images-what the image becomes in memory when actually executed. It runs completely isolated host environment by default, only accessing host files and ports if configured to do so.

Containers run apps natively on the host machine's kernel. They have better performance characteristics than virtual machines that only get virtual access to host resources through a hypervisor. Containers can get native access, each one running in a discrete[分离的] process, taking no more memory than any other executable.

## Containers vs. virual machines

Virtual Machine diagram

![Virtual Machine diagram](https://www.docker.com/sites/default/files/VM%402x.png)

Virtual machines run guest operating systems -- note the OS layer in each box. This is resource intensive[密集的], and the resulting disk image and application state is an entanglement[纠葛] of OS settings, system-installed dependencies, OS security patches, and other easy-to-lose, hard-to-replicate[复制] ephemera.

Container diagram

![Virtual Machine diagram](https://www.docker.com/sites/default/files/Container%402x.png)

Containers can share a single kernel, and the only information that needs to be in a container image is the executable and its package dependencies, which never need to be installed on the host system. These processes run like native processes, and you can manage them individually by running commands like **docker ps** -- just like you would run **ps** on Linux to see active processes. Finally, because they contain all their dependencies, there is no configuration entanglement[纠葛]; a containerized app "run anywhere."
 


