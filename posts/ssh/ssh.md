# Connecting via SSH

## What is SSH

_Secure Shell_ (SSH) is a network protocol that allows for secure communication between two computers over the network.

We will need an SSH server on our Pis, and an SSH client on our local computer

## Installation

Let's install the SSH server on our Pis first

``` sh
apt install openssh-server
```

`HINT:` Installing new software requires elevated privileges. You will need to prefix the commands above with `sudo` unless running as the root user.

And let's make sure it's running

``` sh
service ssh status
```

If the service is running it should say something like

``` sh
Active: active (running) since Sat 2020-09-19 13:36:46 BST; 1 months 28 days ago
```

Otherwise we can start the service by running:

``` sh
service ssh start
```

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

Apart from executing commands locally, it is also possible to copy files to and from a remote connection

### __Local to Remote__

``` sh
scp /path/to/local/file user@host:/path/to/remote/file
```

### __Remote to Local__

``` sh
scp user@host:/path/to/remote/file /path/to/local/file
```

## `BONUS:` Graphical SSH Clients

Check out some graphical SSH clients. Some have useful features like bookmarking connections, including credentials and having multiple connections open in separate tabs

* Windows: [mRemoteNG](https://mremoteng.org/)
* MacOS: [Terminus](https://www.termius.com/)
