---
title: Linux Kernel - Setting up development environment
description: In this post i'll share my experience in setting up my environment to contribute to the Linux Kernel
author: cotes
date: 2022-05-21 11:33:00 +0800
categories: [Blogging, Free Software]
tags: [kernel]
pin: true
math: true
mermaid: true
---

This series of posts will detail my experience through a course at the University of São Paulo (USP) where our objective is to actively contribute to free software. Our first mission was to make a small contribution to the Linux Kernel!


# Setup

To begin, we followed the [`Flusp Tutorials`](https://flusp.ime.usp.br/kernel/). My first step was to install *libvirt*, a software that manages virtual machines. Then, we set up a virtual machine using a Debian ARM disk image.


# Build 

Next, we cloned the IIO subsystem tree and built it following the tutorials. The only issue I encountered during this part was missing packages, since my current distribution is Manjaro (Arch-based). Afterward, I installed the kernel modules and made minor changes so that my VM would use the newly generated kernel image to boot up.

# Modules and configuration

In the last tutorial, we created a simple Linux Kernel Module and then rebuilt the kernel. Initially, I created the new module files in the IIO subsystem tree and then updated the kernel configuration so that my new module would be recognized by the system. 

Next, I rebuilt the kernel image and modules, followed by installing the new modules. After that, I launched the virtual machine to verify if the kernel version was correct. Lastly, I installed the kernel module inside the VM using the command *modprobe*.


