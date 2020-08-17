# Homelab Setup

## Preface

This document covers the foundation of my homelab environment. All subsequent posts will build on top of this one.

Fields marked as `BONUS` are topics that I will _not_ cover in this series but could be interesting for you to try out for yourself

## Setup

My homelab will run on a cluster of five Raspberry Pis (Version 3, Model B), but since I do not intend on utilizing any of the Pis specialized hardware you will be able to replicate my setup using plain virtual machines.

### Virtualization

In order to follow along I recommend creating at least two virtual machines in a hypervisor of your choice. If you do not have a strong preference I would recommend one of the following:

* VMWare Workstation Player
* Oracle VirtualBox

Both of them are free of charge and highly robust.

### Choice of Operating System

My Pis will be running Raspberry Pi OS (formerly known as Raspbian), a fork of Debian that runs on ARM chips.

For your own setup any of the following would be a solid choice for a home server

* __Debian family__: Ubuntu Server, Debian Stable (Buster), Debian Testing (Bullseye)
* __Red Hat family__: CentOS, Fedora Server
* OpenSUSE Leap

Read up on each operation system to find out about their specific strengths and weaknesses.
Several distributions will let you browse their package repositories online. Use these to find out what software is available out of the box.
For example you can browse OpenSUSE packages [here](https://software.opensuse.org/find)

`BONUS:` For an additional challenge try installing one from each group

`HINT:` You can use [pkgs.org](https://pkgs.org/) to find and compare specific package versions on several popular Linux distributions.

[pkgs.org](/posts/pkgs.org.png)

---

## Choice of Operating System
    * Ubuntu Server 20.04
    * 5 year support period
    * Good documentation
    * Good community

### Alternatives
    * Debian
    * Red Hat family (CentOS/RHEL, Fedora)
    * OpenSUSE Leap

## Setup

### Acquire installation media

### Virtualization
    * Install hypervisor (VirtualBox, VMWare Player)
    * Setup two virtual machine with low specs (1 core, 512 MB)

### Configuration
    * Set hostnames
    * Set static ips

### Additional Services
    * Install Cockpit
    * Install Docker

### Configure Host
    * Add host entries
    * Add ssh config
