# Overview

![Raspberry Pi Cluster](/posts/overview/images/pi-cluster.jpg)

## My Setup

My homelab consists of a cluster of five Raspberry Pis (Version 3 Model B) running Raspberry Pi OS (formerly known as Raspbian) which is a derivative of Debian that runs on ARM processors.

I won't be using any of the Pi's special hardware features, so you'll be able to follow along at home on nearly any GNU/Linux distribution.

## Post Installation Steps

### __Hostnames__

Giving our hosts specific hostnames will help us identify them easily. Make sure each host was a unique name.

In my case I will name each host after the color of it's case.

Type the following example into the terminal, substituting the host name with whatever you wish:

``` sh
hostname pi-red
```

### __Static IP address__

_This step may differ on your distribution_. On Raspberry Pi OS we'll do the following

Edit `/etc/dhcpcd.conf` using `nano` or any other text editor of your choice

``` sh
nano /etc/dhcpcd.conf
```

Add the following lines to set the IP to `192.168.1.xxx` where `xxx` is an integer between 1 & 254. Ensure all VMs have unique IP addresses

In this example we will set the ip to `192.168.1.100`

``` sh
interface eth0
static ip_address=192.168.1.100
```

Changes will take effect after rebooting

## Next Steps

After those two steps, all following recipes can be done fully remotely over the network. You may do them in any order you want.

Go forth and tinker!
