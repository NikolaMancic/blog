# Connecting via SSH

## What is SSH

...

## Installation

This will allow us to connect to our servers remotely via the SSH protocol. Further steps will

``` sh
apt install openssh-server
```

`HINT:` Installing new software requires root privileges. You will need to prefix the commands above with `sudo` unless running as the root user.

## Configure the Host

Now we will configure our PC/Laptop to be able to easily connect to our remote hosts.

### __Add Host Entries__

Add DNS entries for your remote systems by editing your host operating system's `hosts` file. Editing requires root/admin privileges

On Linux & macOS the `hosts` file is located in:

``` sh
/etc/hosts
```

On Windows the `hosts` file is located in:

``` sh
C:\Windows\System32\drivers\etc\hosts
```

Add an entry for each host you want to connect to. The syntax is the same on all operating systems.

Example:

``` conf
192.168.1.100   pi-red
192.168.1.101   pi-blue
192.168.1.102   pi-yellow
192.168.1.103   pi-white
192.168.1.104   pi-black
```

### __Create SSH Config__

Create an SSH config file on your PC/Laptop. This file effectively acts as a bookmark for all your frequent SSH connections.
On Windows I recommend using [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (Windows Subsystem for Linux)

In your home folder crate a hidden `.ssh` folder. Inside the folder create a file called `config`.

``` sh
mkdir ~/.ssh
touch ~/.ssh/config
```

Edit the `config` file and add the following content (ensuring it matches the values you entered above)

``` sh
nano ~/.ssh/config
```

``` sh
# Enter an arbitrary name here
Host pi-red

# The host name can either ba a DNS entry that you entered into the host file above or an ip address.
# Use one or the other, but not both
HostName pi-red
HostName 192.168.1.100
```

To verify you can connect successfully enter the following into your shell

``` sh
ssh username@pi-red
```

Substitute `username` with an actual user on your remote system.

You will be prompted to generate an SSH key the first time you try to connect. Respond to the prompt with `yes`

You should now be connected to your remote machine

Verify using:

``` sh
uname -a
```

## Copying files via SSH

...

### __Local to Remote__

...

### __Remote to Local__

...
