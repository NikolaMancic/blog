# __Homelab Setup__

![Raspberry Pi Cluster](/posts/00-homelab-setup/pi-cluster.jpg)

## __Preface__

This document covers the foundation of my homelab environment. All subsequent posts will build on top of this one.

Fields marked as `BONUS` are topics that I will _not_ cover in this series but could be interesting for you to try out for yourself

## __Setup__

My homelab will run on a cluster of five Raspberry Pis (Version 3, Model B), but since I do not intend on utilizing any of the Pis specialized hardware you will be able to replicate my setup using plain virtual machines.

### __Virtualization__

In order to follow along I recommend creating at least two virtual machines in a hypervisor of your choice. If you do not have a strong preference I would recommend one of the following:

* VMWare Workstation Player
* Oracle VirtualBox

Both of them are free of charge and highly robust.

Server operating systems have lower minimum requirements than desktop operating systems. Assigning 1 CPU core and 512MB of RAM will suffice.

Example:

![VMWare Settings](/posts/00-homelab-setup/vmware.png)

### __Choice of Operating System__

My Pis will be running Raspberry Pi OS (formerly known as Raspbian), a fork of Debian that runs on ARM chips.

For your own setup any of the following would be a solid choice for a home server

* __Debian family__: Ubuntu Server, Debian Stable (Buster), Debian Testing (Bullseye)
* __Red Hat family__: CentOS, Fedora Server
* OpenSUSE Leap

Read up on each operation system to find out about their specific strengths and weaknesses. All of the distributions listed above are likely to be encountered in an enterprise setting. The other two distros that are worth mentioning are:

* __Red Hat Enterprise Linux (RHEL)__ - Perhaps the most corporate and enterprise friendly distribution. It is identical to CentOS but also offers commercial support
* __SUSE Linux__ - Identical to OpenSUSE Leap but offers commercial support

Several distributions will let you browse their package repositories online. Use these to find out what software is available out of the box.
For example you can browse OpenSUSE packages [here](https://software.opensuse.org/find)

`BONUS:` For an additional challenge try installing one from each group

`HINT:` Avoid installing GUIs to minimize system requirements

`HINT:` You can use [pkgs.org](https://pkgs.org/) to find and compare specific package versions on several popular Linux distributions.

![pkgs.org](/posts/00-homelab-setup/pkgs.org.png)

## __Post Installation Steps__

### __Package Management__

Every distribution has a package manager and a central package repository from which new software packages and updates are acquired.
Some distributions have the ability to add third party repositories such as PPAs (Personal Package Archive) on Ubuntu or RPM Fusion on Fedora.
It is vital to understand the basics of your package manager before continuing.
To learn more about your package manager, access their man pages using the following commands

``` bash
# Debian, Ubuntu
man apt

# Fedora
man dnf

# CentOS
man yum

# OpenSUSE
man zypper
```

### __SSH__

This will allow us to connect to our servers remotely via the SSH protocol. Further steps will

``` bash
# Debian, Ubuntu
apt install openssh-server

# Fedora
dnf install openssh-server

# CentOS
yum install openssh-server

# OpenSUSE
zypper install openssh
```

`HINT:` Installing new software requires root privileges. You will need to prefix the commands above with `sudo` unless running as the root user.

__The remainder of this series will focus on Raspberry Pi OS. If certain steps are not compatible with your system of choice, consult the documentation or check online for a solution__

### __Hostname__

Giving our VMs specific hostnames will help us identify them easily. Make sure each VM was a unique host name.

In my case I will name each host after the color of it's case.

Type the following example into the terminal, substituting the host name with whatever you wish:

``` bash
hostname pi-red
```

### __Static IP addresses__

Edit `/etc/dhcpcd.conf` using `nano` or any other text editor of your choice

``` bash
nano /etc/dhcpcd.conf
```

Add the following lines to set the IP to `192.168.1.xxx` where `xxx` is an integer between 1 & 254. Ensure all VMs have unique IP addresses
In this example we will set the ip to `192.168.1.100`

``` bash
interface eth0
static ip_address=192.168.1.100
```

Changes will take effect after rebooting

### __`BONUS:` Cockpit__

``` bash
# Install cockpit
apt install cockpit

# Start the cockpit service
systemctl start cockpit

# Check the status of the cockpit service
systemctl status cockpit
```

If started successfully the output of `systemctl status` should contain something like:

```
Active: active (running) since ...
```

## __Configure the Host__

### __Add Host Entries__

Add DNS entries for your remote systems by editing your host operating system's `hosts` file. Editing requires root/admin privileges

On Linux & macOS the `hosts` file is located in:
```
/etc/hosts
```

On Windows the `hosts` file is located in:
```
C:\Windows\System32\drivers\etc\hosts
```

Add an entry for each VM you created. Example:

```
192.168.1.100   pi-red
192.168.1.101   pi-blue
192.168.1.102   pi-yellow
192.168.1.103   pi-white
192.168.1.104   pi-black
```

### __Create SSH Config__

Create an SSH config file on your host operating system. This file effectively acts as a bookmark for all your frequent SSH connections.
On Windows I recommend using [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (Windows Subsystem for Linux)

In your home folder crate a hidden `.ssh` folder. Inside the folder create a file called `config`.

``` bash
mkdir ~/.ssh
touch ~/.ssh/config
```

Edit the `config` file and add the following content (ensuring it matches the values you entered above)

``` bash
nano ~/.ssh/config
```

```
# Enter an arbitrary name here
Host pi-red

# The host name can either ba a DNS entry that you entered into the host file above or an ip address.
# Use one or the other, but not both
HostName pi-red
HostName 192.168.1.100
```

To verify you can connect successfully enter the following into your shell

``` bash
ssh username@pi-red
```

Substitute `username` with an actual user on your remote system.

You will be prompted to generate an SSH key the first time you try to connect. Respond to the prompt with `yes`

You should now be connected to your remote machine

Verify using:

``` bash
uname -a
```

### __`BONUS`: Connecting to Cockpit__

Try connecting to cockpit on your host operating system.

Open a web browser and either type a DNS name or IP address followed by cockpit's default port number 9090

Examples:
* `192.168.1.100:9090`
* `pi-red:9090`

You should see the login page

![cockpit login](/posts/00-homelab-setup/cockpit-login.png)

Enter any valid credentials for the system you're accessing. Once logged in you should see a dashboard

![cockpit dashboard](/posts/00-homelab-setup/cockpit-dashboard.png)

Cockpit gives you an overview of several aspects of your system. Feel free to browse around and learn more [here](https://cockpit-project.org/)

## __Troubleshooting__

![troubleshooting](/posts/00-homelab-setup/troubleshoot.gif)

In the inevitable event that you run into issues it is vital to know how to look for solutions.
Remember that no one knows everything. Knowing how to find answers is a skill in and of itself.
Before asking someone for help, consider trying the following:

* Look at the manual pages for the commands you are trying to use (`man <command-name>`)
* Look at the official documentation for your operating system, or specific service you're troubleshooting
* Search in online forums

## Additional Reading

If your Linux command line skills are a bit rusty you can get a refresher [here](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)

It can be very useful to learn and get comfortable with an extensible text editor such as [Vim](https://www.vim.org/) or [Emacs](https://www.gnu.org/software/emacs/)
