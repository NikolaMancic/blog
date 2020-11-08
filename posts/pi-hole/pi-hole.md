# Network wide ad blocking with Pi Hole

## __About Pi Hole__

Pi Hole is a DNS filter. It's used for network wide ad blocking. It is especially useful for mobile devices that do not have dedicated ad blockers. Bare in mind that it is not a perfect solution and the ad blocking can be a bit hit and miss,

Learn more [here](https://pi-hole.net)

## __Prerequisites__

### __Installing Git__

Git is a source code management system. It is a handy tool that let's us save snapshots of files. Most commonly used for source code and other plain text files, although it does work with any file format. It is likely preinstalled on most systems, but if it is not, let's install it via:

``` sh
sudo apt install git
```

Learn more about git on their [official website](https://git-scm.com)

## __Running Pi Hole__

Pi Hole can run either as a native service or in a docker container. In this article we will chose the latter

The [official GitHub page](https://github.com/pi-hole/docker-pi-hole) has scripts to help us get things up and running. Let's pull the repo via:

``` sh
git clone https://github.com/pi-hole/docker-pi-hole.git
```

As instructed in the "Quick Start" section, let's make a copy of the docker-compose file:

``` sh
# navigate into the cloned folder
cd docker-pi-hole

# copy file
cp docker-compose.yml.example docker-compose.yml
```

Now let's edit the file using your favorite text editor and make some adjustments:

* __Change time zone__: Find the name of your timezone [here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) and set the value. For example: `TZ: 'Europe/London'`

* __Set password__: Uncomment the line for the web password and pick something memorable. For example: `WEBPASSWORD: 'pihole'`

Once we're happy with the settings, let's starting the containers using:

``` sh
docker-compose up --detach
```

`NOTE:` The `docker-compose` command needs to be run in the folder containing the `docker-compose.yml` file

We should now see docker pull down and run the Pi Hole image. Let's check with:

``` sh
docker ps
```

We should see something like this printed out:

```
CONTAINER ID        IMAGE                  COMMAND             CREATED             STATUS                   PORTS                                                                                                  NAMES
b303bd65cde0        pihole/pihole:latest   "/s6-init"          4 minutes ago       Up 4 minutes (healthy)   0.0.0.0:53->53/udp, 0.0.0.0:53->53/tcp, 0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp, 0.0.0.0:67->67/udp   pihole
```

Finally, to check if the ports are configured correctly, let's try to get the contents of our Pi Hole instance with:

```
curl http://localhost
```

If everything is running correctly, we should see some HTML printed on the screen

Alternatively, you can try visiting the admin panel in a web browser on a different device on the same network. You can get the IP address of the Pi Hole host with:

``` sh
ip address show
```

## __Configuring Devices__

Now that we have everything up and running, the last thing we need to do is to configure our devices to use Pi Hole as our DNS provider.

This can be done either on the network router level or device level. As it is not possible to cover every router model and operating system it is best to consult the [official documentation](https://docs.pi-hole.net/main/post-install/) and look up instructions for your particular router and operating system.
